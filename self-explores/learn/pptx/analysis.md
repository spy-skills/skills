# pptx

## Danh gia (Score 8/10)

| Tieu chi | Diem | Ly do |
|----------|------|-------|
| Completeness | 9/10 | Bao phu day du 3 luong cong viec (read, edit, create). SKILL.md 232 dong lam router, editing.md 205 dong huong dan XML workflow, pptxgenjs.md 420 dong lam reference tao moi. 59 files bao gom scripts, validators, XSD schemas ISO-IEC29500. Chua day du hon khi them QA workflow voi verification loop bat buoc. Chi thieu huong dan xu ly animation va transition. |
| Usability | 8/10 | Quick Reference table 3 dong dau SKILL.md la cuc ky hieu qua -- agent doc 3 dong la biet di dau. Decision tree ro rang: read -> markitdown, edit -> editing.md, create -> pptxgenjs.md. Tuy nhien editing.md yeu cau hieu Office XML (namespace, sldIdLst, relationship IDs) -- do la barrier cao cho agent khong co background. pptxgenjs.md thi than thien hon vi dung JavaScript API thong thuong. |
| Modularity | 9/10 | Kien truc module rat tot. Scripts tach rieng tung chuc nang: unpack.py, pack.py, clean.py, add_slide.py, thumbnail.py, soffice.py. Validators co base class (BaseSchemaValidator) va PPTXSchemaValidator ke thua. Shared scripts (office/) dung chung voi docx/xlsx skills. XSD schemas theo chuan ISO-IEC29500-4_2016. Tai lieu tach thanh 3 file doc lap, moi file tu du cho 1 luong cong viec. |
| Safety | 8/10 | Dung defusedxml.minidom thay vi xml.etree.ElementTree (tranh XML bomb attacks). Pack.py co validation + auto-repair truoc khi tao file. PPTXSchemaValidator kiem tra 10 loai loi: XML syntax, namespaces, unique IDs, UUID format, file references, slide layout IDs, content types, XSD compliance, notes references, duplicate layouts. Smart quote handling tu dong trong unpack/pack. Chi thieu: khong co rollback mechanism khi pack that bai, khong co backup tu dong truoc khi edit. |

**Tong diem: 8/10** -- Day la mot skill production-grade voi kien truc suy nghi ky luong, nhung do phuc tap cua Office XML nen co barrier cao cho nguoi dung va agent moi.

## Uu & Nhuoc diem

### Uu diem

1. **3-path decision tree trong Quick Reference la thiet ke tuyet voi.** 3 dong dau SKILL.md (`Read/analyze -> markitdown`, `Edit -> editing.md`, `Create -> pptxgenjs.md`) cho phep agent quyet dinh ngay lap tuc dung tool nao, khong can doc het 232 dong. Day la pattern "router document" -- SKILL.md khong lam viec truc tiep ma chi dinh huong. Thiet ke nay giam token cost vi agent chi can doc file phu hop voi task.

2. **Design philosophy nhung truc tiep vao document skill la quyet dinh tao bao va dung dan.** Muc "Design Ideas" (dong 51-138) khong phai la tai lieu tham khao -- no la opinionated guide: "Don't create boring slides", "NEVER use accent lines under titles -- hallmark of AI-generated slides", bang mau cu the voi hex codes, font pairings, spacing rules. Day la dieu hiem thay trong document processing skills -- thuong thi skills chi focus vao ky thuat, nhung skill nay hieu rang output cua PPTX la visual va can huong dan tham my.

3. **QA workflow bat buoc voi "assume there are problems" mindset.** Muc QA (dong 141-204) khong phai optional -- no yeu cau: (a) content QA bang markitdown + grep placeholder text, (b) visual QA bang subagent voi fresh eyes, (c) verification loop "fix -> re-verify -> repeat". Cau "Your first render is almost never correct" va "If you found zero issues on first inspection, you weren't looking hard enough" cho thay kinh nghiem thuc te ve cac loi LLM thuong gap khi tao slides. Day la self-aware design.

4. **Office XML validator co 10 buoc kiem tra voi auto-repair.** PPTXSchemaValidator kiem tra: XML well-formedness, namespace correctness, unique IDs (per-file va global), UUID format (regex validation), file references (rels files), slide layout IDs (cross-reference voi slideMaster), content types, XSD schema compliance, notes slide references (uniqueness), duplicate slide layouts. BaseSchemaValidator cung cap shared logic cho cac Office format khac. Day la defense-in-depth approach.

5. **Subagent parallelization duoc thiet ke tu dau.** Editing.md chi ro: "If available, use them here. Each slide is a separate XML file, so subagents can edit in parallel." Visual QA cung yeu cau subagent ("USE SUBAGENTS -- even for 2-3 slides. You've been staring at the code and will see what you expect, not what's there."). Day la skill hiem hoi co explicit subagent strategy.

### Nhuoc diem

1. **Editing workflow yeu cau hieu sau ve Office XML -- barrier cao cho agent.** Editing.md huong dan truc tiep manipulate XML: `<p:sldIdLst>`, `<a:rPr>`, `<a:buChar>`, `xml:space="preserve"`, namespace prefixes. Agent can biet: relationship IDs, content types, slide master hierarchy, run properties. Day la muc do phuc tap tuong duong voi mot Office XML developer, khong phai mot general-purpose agent. Ket qua la editing workflow de loi hon creating workflow (pptxgenjs) vi JavaScript API truu tuong hoa het cac chi tiet XML.

2. **Reference files qua lon -- 420 dong pptxgenjs.md va 205 dong editing.md.** Khi agent can doc editing.md + SKILL.md, tong cong la 437 dong = ~3000 tokens chi de hieu workflow. Neu can tao moi, pptxgenjs.md them 420 dong = ~3000 tokens nua. Tong context cost cho mot task phuc tap co the len 6000+ tokens chi tu tai lieu. Cac file nay co the duoc tach nho hon (vd: pptxgenjs.md co the tach thanh basic.md + charts.md + advanced.md) de giam context khi agent chi can mot phan.

3. **Khong co error recovery workflow khi pack/validate that bai.** Pack.py co validation va auto-repair, nhung khong co tai lieu huong dan agent lam gi khi validation van that bai sau auto-repair. Cac loi nhu "invalid UUID", "duplicate slide layout reference", "orphaned notes slide" can huong dan cu the de fix. Hien tai agent phai tu suy luan cach sua -- day la diem yeu khi gap loi phuc tap.

4. **Thieu huong dan ve animation, transition, va embedded media.** PPTX thuong co animations (entrance, exit, emphasis), slide transitions, embedded video/audio. Skill khong de cap den cac thanh phan nay. Khi agent gap file co animation, khong co huong dan de preserve hoac modify chung trong editing workflow.

## Kha nang tich hop vao he thong hien tai

Skill nay co kha nang tich hop cao nho cac yeu to sau:

- **Shared infrastructure voi docx va xlsx skills.** Thu muc `scripts/office/` (pack.py, unpack.py, validate.py, soffice.py, validators/) duoc dung chung. BaseSchemaValidator la base class chung. XSD schemas theo chuan ISO-IEC29500 ho tro ca 3 format. Tich hop mot skill Office tu dong co loi cho cac skill khac.

- **Dependencies pho bien va de cai.** markitdown (pip), Pillow (pip), pptxgenjs (npm), LibreOffice (system), Poppler (system). Tat ca deu la open-source, khong co proprietary dependency ngoai skill code.

- **Subagent-ready architecture.** Cac slide la file XML doc lap, cho phep parallel editing. QA workflow yeu cau subagent voi fresh eyes. Day la thiet ke phu hop voi multi-agent orchestration systems.

- **Pipeline integration.** Read path (markitdown) tra ve markdown -- de pipe vao cac skill khac (summary, email, report). Create path (pptxgenjs) nhan input tu bat ky nguon nao va output .pptx file. Edit path hoat dong tren unpacked directory -- co the tich hop voi version control.

- **De mo rong.** Them validator moi chi can ke thua BaseSchemaValidator. Them script moi chi can dat vao scripts/. Them design themes chi can cap nhat bang mau trong SKILL.md.

Diem can luu y khi tich hop: editing workflow yeu cau agent co kha nang xu ly XML -- can kiem tra agent co du kha nang truoc khi route task editing. Nen uu tien pptxgenjs path cho create tasks vi no than thien hon.

## Ghi chu ky thuat (Technical Decisions)

1. **SKILL.md la router, khong phai executor.** Day la quyet dinh kien truc quan trong nhat. SKILL.md 232 dong chi lam 3 viec: (a) Quick Reference table de route, (b) Design philosophy de huong dan tham my, (c) QA workflow de dam bao chat luong. Moi cong viec thuc te duoc uy quyen cho editing.md hoac pptxgenjs.md. Pattern nay giam cognitive load va cho phep moi file duoc toi uu hoa doc lap.

2. **Hai con duong tao PPTX hoan toan khac nhau.** Edit path dung Python + XML manipulation (unpack -> edit XML -> pack). Create path dung Node.js + pptxgenjs API. Day la quyet dinh thuc dung: edit template can preserve formatting goc (XML la cach duy nhat), tao moi can productivity (JavaScript API nhanh hon viet XML tay). Trade-off la agent can 2 runtime environments (Python + Node.js).

3. **defusedxml thay vi xml.etree.ElementTree.** Editing.md ghi ro: "Use defusedxml.minidom, not xml.etree.ElementTree (corrupts namespaces)." Day la quyet dinh ca ve security (chong XML bomb) va correctness (preserve namespace prefixes). xml.etree strips namespace prefixes khi parse, gay loi khi pack lai.

4. **Validator voi auto-repair trong pack.py.** Pack.py khong chi validate -- no co auto-repair. Day la quyet dinh giam friction: thay vi bao loi va yeu cau agent sua thu cong, no tu dong sua cac loi pho bien (duplicate IDs, missing content types). Chi bao loi khi khong the tu sua.

5. **Design opinions la mandatory, khong phai optional.** "NEVER use accent lines under titles -- hallmark of AI-generated slides" la mot lenh, khong phai goi y. Day la quyet dinh chong "AI-looking output" -- skill nay hieu rang PPTX output thuong bi danh gia ve mat visual, va default AI output thuong tro nen nhan dien duoc theo thoi gian.

6. **Visual QA bat buoc dung subagent.** Khong phai goi y ma la yeu cau: "USE SUBAGENTS -- even for 2-3 slides." Ly do duoc giai thich: "You've been staring at the code and will see what you expect, not what's there." Day la quyet dinh chong confirmation bias -- mot van de pho bien khi LLM tu danh gia output cua minh.

7. **Thumbnail.py chi de chon layout, khong de QA.** Editing.md ghi ro: "Use for template analysis only. For visual QA, use soffice + pdftoppm to create full-resolution individual slide images." Day la su phan biet quan trong: thumbnail (thap resolution, grid) cho overview nhanh, soffice render (cao resolution, tung slide) cho kiem tra chi tiet.

8. **Smart quote handling tu dong.** Unpack.py thay unicode quotes bang XML entities, pack.py encode lai. Edit tool chuyen smart quotes thanh ASCII. Day la quyet dinh tranh loi encoding -- mot nguon loi pho bien khi edit Office XML bang text tools.

9. **XSD schemas theo chuan ISO-IEC29500-4_2016.** Skill mang theo schemas chinh thuc (pml.xsd, dml-main.xsd, etc.) de validate offline. Day la quyet dinh dam bao output compliance voi Office Open XML standard, khong chi "chay duoc" ma con "dung chuan."

10. **add_slide.py thay vi manual copy.** Script nay xu ly: tao relationship file, cap nhat Content_Types.xml, generate unique IDs, xu ly notes references. Editing.md canh bao: "Never manually copy slide files -- the script handles notes references, Content_Types.xml, and relationship IDs that manual copying misses." Day la automation cho cac buoc de loi nhat trong Office XML editing.
