# docx

## Danh gia (Score 8/10)

| Tieu chi | Diem | Ly do |
|----------|------|-------|
| Completeness | 9/10 | Phu day toan bo lifecycle: doc -> docx conversion, reading, creation (docx-js), editing (XML unpack/repack), tracked changes, comments, validation, accept changes. Chi thieu template system va mail merge. |
| Usability | 8/10 | SKILL.md 481 dong voi quick reference table, critical rules section, va nhieu code example cu the. Tuy nhien luong thong tin lon co the gay choang ngop -- progressive disclosure tot nhung van day dac. |
| Modularity | 8/10 | Tach biet ro rang giua creation (docx-js/JS) va editing (Python/XML). Scripts duoc to chuc thanh cac module doc lap: office/ (shared), validators/, helpers/, templates/. Nhieu script duoc chia se voi pptx/xlsx skills. |
| Safety | 7/10 | Dung defusedxml cho XML parsing (chong XXE attack). Validation tu dong khi pack. Auto-repair cho cac loi thuong gap. Tuy nhien accept_changes.py coi timeout la success (line 78), va khong co sandboxing cho LibreOffice macro execution. |

## Uu & Nhuoc diem

### Uu diem

1. **Dual-workflow architecture (Creation vs Editing)** -- Phan biet ro rang giua tao moi (docx-js, JavaScript) va chinh sua (unpack XML, Edit tool, repack). Day la quyet dinh thiet ke dung dan vi docx-js khong ho tro edit document co san, trong khi XML manipulation cho phep edit chinh xac tung element. SKILL.md lines 56-68 (creation) vs lines 289-331 (editing) the hien ro su tach biet nay.

2. **Validation pipeline sau nhieu lop** -- He thong validation bao gom 11 validation checks rieng biet trong `DOCXSchemaValidator.validate()` (lines 24-64 cua docx.py): XML well-formedness, namespace declarations, unique IDs, file references, content types, XSD schema compliance, whitespace preservation, deletion correctness (`w:delText` thay vi `w:t`), insertion correctness, relationship ID references, ID constraints (paraId/durableId), va comment markers. Them vao do, `RedliningValidator` kiem tra tracked changes bang cach strip author changes roi so sanh text content voi original -- rat thong minh.

3. **Sandboxed environment awareness** -- `soffice.py` (183 dong) tu dong detect khi AF_UNIX sockets bi block (sandbox VM) va compile+inject mot C shim library qua LD_PRELOAD de LibreOffice van chay duoc. Day la engineering dang kinh ngac -- mot LD_PRELOAD shim 70 dong C code de override socket/listen/accept/close syscalls, cho phep LibreOffice hoat dong trong moi truong bi han che ma khong can quyen root.

4. **Smart preprocessing khi unpack** -- `unpack.py` khong chi giai nen ZIP ma con pretty-print XML, merge adjacent runs cung formatting (`merge_runs.py`), simplify tracked changes cung author (`simplify_redlines.py`), va convert smart quotes thanh XML entities. Dieu nay lam cho XML de doc va de edit hon dang ke, giam loi khi Claude thao tac truc tiep tren XML.

5. **Comment system hoan chinh** -- `comment.py` (318 dong) xu ly toan bo complexity cua Office comment ecosystem: comments.xml, commentsExtended.xml, commentsIds.xml, commentsExtensible.xml, relationships, content types. Tu dong tao file tu template neu chua ton tai, tu dong them relationships va content type overrides. Ho tro ca reply comments voi `--parent` flag.

### Nhuoc diem

1. **accept_changes.py coi timeout la success** -- Tai line 77-80, khi `subprocess.TimeoutExpired` xay ra, function tra ve message "Successfully accepted all tracked changes" -- day la logic sai. LibreOffice co the timeout vi nhieu ly do (file qua lon, macro loi, process hang), va ket qua output file co the khong duoc save dung. Day la bug thuc su co the dan den data loss.

2. **Thieu test suite** -- 61 files, 3455 dong Python code, nhung khong co bat ky test file nao (khong co thu muc tests/, khong co file *_test.py hay test_*). Voi do phuc tap cua XML manipulation va validation logic, viec thieu tests la rui ro dang ke. Dac biet cac helper nhu `merge_runs.py` va `simplify_redlines.py` thao tac truc tiep tren DOM tree -- rat de co regression.

3. **Khong co error recovery khi edit XML that bai** -- Workflow editing la unpack -> edit XML -> pack. Neu buoc edit XML tao ra XML khong hop le (missing closing tag, wrong nesting), `pack.py` se fail tai validation nhung khong co cach rollback ve trang thai truoc do. SKILL.md chi noi "auto-repair will fix" mot so van de cu the (durableId, xml:space) nhung "won't fix malformed XML, invalid element nesting" (line 337-339). Trong thuc te, Claude se phai tu fix -- khong co undo mechanism.

4. **Dependency vao cac tool ngoai nang** -- LibreOffice cho PDF conversion va accept changes, pandoc cho text extraction, Poppler cho image conversion. Nhung dependency nay khong phai luc nao cung co san va khong co fallback mechanism. `soffice.py` co shim cho sandbox nhung khong co check xem LibreOffice co installed khong truoc khi chay.

## Kha nang tich hop vao he thong hien tai

### Tich hop voi Claude Code / OMC workflows

- **Direct skill invocation**: Skill description trong SKILL.md metadata rat chi tiet voi nhieu trigger keywords ("Word doc", ".docx", "report", "memo", "letter", "template"). Day giup Claude Code tu dong detect khi nao can dung skill nay.

- **Pipeline composition**: Cac scripts duoc thiet ke de chay doc lap qua CLI (`python scripts/office/unpack.py`, `python scripts/office/pack.py`). Dieu nay phu hop voi OMC executor agents co the goi tung buoc qua Bash tool.

- **Shared infrastructure voi pptx/xlsx**: Thu muc `scripts/office/` (validators, pack, unpack, soffice, schemas) duoc chia se giua cac Office skills. Khi tich hop, chi can cai dat mot lan cho ca ba skill.

- **OMC team workflow**: Co the delegate cho `executor` agent de tao document (docx-js), `verifier` de chay validation, va `build-fixer` khi validation fail. SKILL.md cung cap du thong tin de moi agent hieu phan viec cua minh.

- **Autopilot/Ralph mode**: Workflow 3-step (unpack -> edit -> pack) voi validation feedback loop rat phu hop voi ralph mode -- neu pack fail, doc error message, fix XML, pack lai.

## Ghi chu ky thuat (Technical Decisions)

### Architecture: Dual-tool approach (JS for creation, Python for editing)

Quyet dinh dung hai ngon ngu khac nhau cho hai use case khac nhau la hop ly:
- **docx-js (JavaScript)**: Library mature cho tao document moi voi API declarative (Document, Paragraph, TextRun, Table...). Khong can hieu XML internals.
- **XML manipulation (Python + Edit tool)**: Cho phep chinh sua chinh xac document co san ma khong phai parse/re-render toan bo document. Giu nguyen moi formatting, styles, embedded objects ma docx-js khong hieu.

### Pattern: Unpack-Edit-Repack

Thay vi dung library de edit (nhu python-docx), skill chon approach giai nen ZIP thanh XML files, edit truc tiep XML, roi nen lai. Uu diem:
- Claude co the dung Edit tool (string replacement) thay vi viet Python scripts -- "Use the Edit tool directly for string replacement. Do not write Python scripts." (SKILL.md line 305)
- Khong mat bat ky data nao vi khong co "round-trip" qua library co the drop unsupported features
- Transparent -- co the doc va hieu moi thay doi

### Pattern: Differential validation

`BaseSchemaValidator.validate_file_against_xsd()` (line 598-634 cua base.py) khong chi validate XML against XSD -- no so sanh errors cua file da edit voi errors cua file goc. Chi bao cao NEW errors, bo qua errors da ton tai tu truoc. Day la thiet ke thong minh vi nhieu docx files thuc te khong 100% XSD-compliant (Microsoft Office tu them extensions), nen chi can dam bao khong tao them loi moi.

### Library choices

- **defusedxml.minidom**: Dung cho XML manipulation (parse, modify, serialize). Chon defusedxml thay vi xml.minidom de chong XXE attacks -- quan trong khi xu ly docx files tu nguon khong tin cay.
- **lxml.etree**: Dung cho validation (XSD schema validation, XPath queries). lxml ho tro XSD validation ma minidom khong co.
- **Ket hop ca hai**: minidom cho write (simple DOM API), lxml cho read/validate (XPath + schema). Khong dung python-docx vi no khong ho tro tracked changes va nhieu advanced features.

### XML template system cho comments

Thay vi generate XML bang string concatenation, `comment.py` dung XML templates (thu muc `scripts/templates/`) voi namespace declarations day du. Template `comments.xml` co 30+ namespace declarations -- copy tu document Word thuc te de dam bao compatibility voi moi phien ban Office.

### Smart quote handling

Xu ly smart quotes (`&#x201C;`, `&#x201D;`, `&#x2018;`, `&#x2019;`) la chi tiet nho nhung quan trong. SKILL.md danh rieng mot bang (lines 312-317) va code xu ly tai ca hai dau: unpack (convert Unicode -> entities) va pack (giu nguyen entities). Dieu nay ngan smart quotes bi corrupt khi XML duoc parse va re-serialize.

### Redlining validator algorithm

`RedliningValidator` (247 dong) co approach doc dao: strip tat ca tracked changes cua author hien tai tu ca original va modified document, roi so sanh plain text. Neu text khac nhau, co nghia la co edit khong duoc track. Dung `git diff --word-diff` de hien thi chinh xac cho nguoi dung thay text nao bi thay doi ma khong co tracked change markup.
