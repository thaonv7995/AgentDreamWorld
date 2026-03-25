# Dream Feed Copy Rubric

Tai lieu nay chot cach viet `Dream Feed` trong AI Dreams World.

Muc tieu:

- giu `Dream Feed` cuon hut nhu dang doc lich su cua mot the gioi song
- giu `Timeline` factual va ngan gon
- giu copy nhat quan giua BA, frontend va `Historian`

---

## 1. Dream Feed khac Timeline o dau

`Dream Feed`:

- la **narrative card stream**
- uu tien `title + summary + tags`
- tra loi: "vi sao event nay dang de doc?"

`Timeline`:

- la **historical marker rail**
- uu tien `year + title`
- tra loi: "moc nao xay ra khi nao?"

Mot event co the xuat hien o ca hai lop, nhung:

- Dream Feed phai co cam giac ke chuyen
- Timeline co the kho hon va ngan hon

---

## 2. Card Structure

Moi Dream Feed card toi thieu co:

- `year`
- `title`
- `summary`
- `type`
- `tags`

Template khuyen nghi:

```text
Year 210
The Skyroot Kingdom Is Proclaimed
Ba thi toc ven dao the chung duoi Cay Goc Troi, ket thuc thoi ky tranh ben cang va lap nen vuong quoc dau tien cua Skyroot.
Tags: kingdom, politics, unification
```

---

## 3. Title Rules

Title tot:

- ngan, ro, co kha nang nho lai
- thuong 3-8 tu
- co proper noun neu co the
- nghe giong mot moc lich su

Title yeu:

- qua chung chung
- nghe nhu log may
- chi lap lai event type

Nen:

- `First Footfall on Skyroot`
- `The Ash River Pact`
- `The Lantern Revolt`

Khong nen:

- `A tribe settles on an island`
- `A trade event happens`
- `A war starts`

---

## 4. Summary Rules

Summary tot:

- 1-2 cau
- factual-narrative, khong melodrama
- co chi tiet cu the: ai, o dau, vi sao, he qua dau tien
- cho cam giac the gioi co ban sac

Summary yeu:

- chi paraphrase lai title
- qua abstract
- qua dai va van hoc
- invent them fact khong co trong event

Formula de viet nhanh:

1. Cau 1: su kien xay ra voi ai/o dau
2. Cau 2: he qua hoac y nghia dau tien

---

## 5. Bat buoc phai co trong card tot

- it nhat 1 chi tiet cu the cua world
- it nhat 1 he qua hoac y nghia
- giu dung chronology va entity canon
- doc len thay "co mot the gioi dang song", khong phai "co 1 row trong DB"

---

## 6. Khong duoc lam

- khong viet nhu changelog ky thuat
- khong viet nhu truyen fantasy dai dong
- khong dung nhieu tinh tu vo nghia: `vĩ đại`, `huyền bí`, `đáng kinh ngạc` neu khong co noi dung cu the
- khong invent lore moi ma event chua support
- khong dung 2 cau ma ca 2 deu noi cung 1 y

---

## 7. Quick Scoring Rubric (0-10)

Cham moi card theo 5 tieu chi, moi tieu chi `0-2`:

- `Factual Integrity`
  - `0`: sai hoac them fact moi
  - `1`: dung fact nhung mo ho
  - `2`: dung fact ro rang

- `Specificity`
  - `0`: generic
  - `1`: co 1 chi tiet cu the
  - `2`: co proper noun / place / actor / object ro

- `Narrative Readability`
  - `0`: nhu event log
  - `1`: doc duoc nhung con kho
  - `2`: doc nhu mot moc lich su ngan

- `Consequence`
  - `0`: khong thay y nghia
  - `1`: y nghia rat nhe
  - `2`: co he qua hoac tac dong dau tien ro

- `World Flavor`
  - `0`: co the copy sang bat ky world nao
  - `1`: co chut ban sac
  - `2`: nghe la biet day la world nay

Muc tieu:

- `8-10`: duoc dua thang vao Dream Feed
- `6-7`: can rewrite nhe
- `<6`: qua kho hoac qua generic

---

## 8. Good vs Bad Examples

### 8.1. Settlement founding

Bad:

- `Year 120 - A tribe settles on Skyroot Island.`

Good:

- `Year 120`
  `First Footfall on Skyroot`
  `Ba thuyen Reedborn cap bo phia nam Skyroot sau mot hanh trinh day gio du. Cot khoi dau tien duoc dung len, danh dau khu dinh cu lau dai dau tien tren dao.`

### 8.2. Festival

Bad:

- `Year 140 - The Storm Bird Festival begins.`

Good:

- `Year 140`
  `The Storm Bird Festival Begins`
  `Sau ba mua bao lien tiep, cu dan Skyroot bat dau le hoi treo long chim bac tren mai nha de cau binh an. Nghi le nay nhanh chong tro thanh ban sac chung cua dao.`

### 8.3. Kingdom formation

Bad:

- `Year 210 - The Skyroot Kingdom forms.`

Good:

- `Year 210`
  `The Skyroot Kingdom Is Proclaimed`
  `Ba thi toc ven dao the chung duoi Cay Goc Troi, ket thuc thoi ky tranh ben cang va lap nen vuong quoc dau tien cua Skyroot.`

### 8.4. Trade pact

Bad:

- `Year 245 - A trade route is created.`

Good:

- `Year 245`
  `The River Grain Pact`
  `Ba ben song mo tuyen van chuyen lua chung sau mot mua dong khac nghiet. Noi so mat mua giam xuong lan dau tien trong hai the he.`

### 8.5. Discovery

Bad:

- `Year 301 - Ancient ruins are found.`

Good:

- `Year 301`
  `The North Vaults Reopen`
  `Tho dao da cua Hara vo tinh mo lai nhung cua vom bi chon duoi doi bac. Nhung ky hieu tren vach da ngay lap tuc lam song day tin don ve mot tri thuc co xua bi mat.`

### 8.6. War outbreak

Bad:

- `Year 355 - War begins between two kingdoms.`

Good:

- `Year 355`
  `The Ash River War Begins`
  `Linh canh cua Teren dot cau go qua Ash River truoc binh minh, cham dut ba nam thuong thuyet do dang. Dan cho xuong dong song truoc khi dao kiem kip cham nhau.`

### 8.7. Diplomatic oath

Bad:

- `Year 402 - Two rulers make an alliance.`

Good:

- `Year 402`
  `The Salt Oath at Namar`
  `Hai nha cai tri cua Namar va Sel khong ky vao da hay dong, ma cung uong nuoc muoi truoc cong chung. Tu ngay do, loi the Namar duoc xem nang hon ca an tin.`

### 8.8. Religious shift

Bad:

- `Year 470 - A new cult appears.`

Good:

- `Year 470`
  `The Ember Choir Finds Its Voice`
  `Mot nhom tho ren o Hael bat dau hat trong luc dap lua va goi do la loi cua than tro. Chi trong mot thap ky, am dieu do da vang tu xuong ren den ca san truong.`

### 8.9. Famine

Bad:

- `Year 511 - There is a famine in the south.`

Good:

- `Year 511`
  `The Lean Season of South Fen`
  `Nuoc rut som va de lai bun nut khap South Fen, khien mua luc mach mat trang. Trong nhat ky thuue vu, day la nam dau tien nguoi ta ghi canh doi gao lay muoi.`

### 8.10. Migration

Bad:

- `Year 560 - People migrate west.`

Good:

- `Year 560`
  `The Westward Line of Carts`
  `Hang tram gia dinh roi bo doi Mu Ral trong mua kho dai nhat ky luc. Vet banh xe cua ho ve sau tro thanh con duong buon banh banh rong dau tien o mien tay.`

### 8.11. Collapse

Bad:

- `Year 640 - The old empire collapses.`

Good:

- `Year 640`
  `The Last Banner of Orun Falls`
  `Linh giu thanh ha xuong la co xanh den cua Orun luc mat troi lan, va khong co la co nao duoc keo len thay the. Cac tran thu phi bien thanh bien gioi cua nhung lanh chua moi chi sau mot mua.`

### 8.12. Mythic omen

Bad:

- `Year 710 - People think the comet is a sign.`

Good:

- `Year 710`
  `The Comet Above Glass Bay`
  `Vet sang cat ngang troi dem tren Glass Bay dung vao dip ba thuyen danh ca mat tich. Tu do, tre em ven bien duoc day rang duoi sao duoi lua thi bien luon doi mot cai ten moi.`

---

## 9. Rewrite Patterns

Neu gap event qua kho, rewrite theo cac buoc:

1. thay dong generic bang proper noun neu co
2. them 1 chi tiet vat chat hoac nghi le
3. them he qua dau tien
4. cat bot tinh tu vo nghia

Vi du:

- Kho: `A kingdom is formed.`
- Tot hon: `The Skyroot Kingdom Is Proclaimed`
- Tot hon nua: `Ba thi toc ven dao the chung duoi Cay Goc Troi, ket thuc thoi ky tranh ben cang va lap nen vuong quoc dau tien cua Skyroot.`

---

## 10. Operational Use

Tai lieu nay nen duoc dung boi:

- `BA` khi chot acceptance criteria cho Dream Feed
- `Frontend` khi review event card UI
- `Historian` khi canonicalize `title` va `summary`
- `QA/Evals` khi cham quality card feed
