# Dream Feed Polyphonic Example

Tài liệu này là một bộ `Dream Feed` mẫu cho **một world duy nhất**, nhưng được viết theo đúng tinh thần **multi-agent polyphonic**.

Mục tiêu:

- chứng minh `Dream Feed` không nên đọc như một timeline khô
- cho thấy nhiều agent khác nhau đang cùng kéo thế giới theo các hướng khác nhau
- cung cấp reference cho BA, prompt design, frontend card design, và evals

Lưu ý quan trọng:

- đây là **polyphonic sample ở cấp world experience**, không phải mô tả scheduler nội bộ theo từng tick
- trong runtime thực tế, không phải cả 10 agent đều active cùng một lúc
- nhưng ở cấp trải nghiệm người đọc, `Dream Feed` tốt phải cho cảm giác thế giới đang được nhiều lực khác nhau cùng viết nên

---

## World: Asterra

**Asterra** là một thế giới của biển mặn, rừng rễ khổng lồ, sông tro và những cơn bão dường như nhớ mặt người.

Các vùng chính:

- `Skyroot`: quần đảo rễ đen mọc thẳng khỏi mặt biển
- `South Fen`: vùng đầm lầy và ruộng lúa trắng ở phương nam
- `Ash River`: con sông chở tro khoáng từ nội địa ra biển
- `North Vaults`: vành đai hầm đá cổ chôn dưới băng muối phương bắc

Các civilization chính:

- `Reedborn`: dân biển và dân thuyền của Skyroot
- `Namar`: các thành muối ở bờ tây
- `Teren`: các đô thị nông-sông của Ash River
- `Hael`: vùng thợ rèn, lò nung và mỏ đá ở phía đông
- `Orun`: đế chế biên giới từng kiểm soát phần lớn đường bộ trung tâm

---

## How To Read This File

Mỗi card có:

- `Primary motion`: agent đẩy chính của event
- `Echoes`: các agent khác đang cộng hưởng vào cùng card đó
- `Feed copy`: đoạn copy nên hiện ra trên Dream Feed

Trong thực tế:

- `Guardian` là lớp giữ coherence, nên không đứng tên như source cảm xúc của card
- `Historian` là lớp biên tập canon, nên đảm bảo `title + summary` đọc được và đúng fact

Nói cách khác:

- `Primary motion` cho thấy lực sáng tạo chính
- `Echoes` cho thấy thế giới đang được nhiều agent kéo cùng lúc
- `Guardian + Historian` là hai bàn tay vô hình giữ cho tất cả không vỡ

---

## 10-Agent Surface Model

Trong project này, 10 agent không nên xuất hiện trên `Dream Feed` như 10 giọng đọc ngang hàng. Vai trò của họ trên feed nên được cảm như sau:

- `Creator`: mở đất, mở biển, mở scale của world
- `Civilization`: dựng trật tự, quyền lực, đường biên, vương quyền
- `Storyteller`: làm cho world có khoảnh khắc đáng nhớ ở cấp con người
- `Culture`: tạo phong tục, tên gọi, lễ hội, dấu hiệu nhận diện
- `Myth`: phủ nghĩa thiêng, lời đồn, biểu tượng, điềm báo
- `Ecology`: đổi nhịp sống bằng mùa, nước, bệnh của đất, dịch chuyển sinh cảnh
- `Economy`: làm lộ ra quyền lực của tài nguyên, tuyến đường, sự thiếu hụt và trao đổi
- `Chaos`: cắt đứt trạng thái ổn định và tạo cảm giác lịch sử có thể rẽ hướng
- `Historian`: chọn cái gì đủ đáng nhớ để thành canon và rewrite cho đọc được
- `Guardian`: đảm bảo mọi thứ vẫn đúng logic world, đúng progression, đúng reference

Vì vậy, một card `Dream Feed` lý tưởng thường có:

- một `Primary motion` rõ ràng
- một hoặc nhiều `Echoes`
- dấu tay vô hình của `Historian` và `Guardian`

---

## Era I – First Smoke Over Salt Water

### Year 018 — Khói đầu tiên trên Skyroot

`Primary motion: Creator` · `Echoes: Ecology, Storyteller`

Biển quanh Skyroot phẳng như kim loại đen vào buổi sáng ba chiếc thuyền Reedborn cập bờ. Đến giữa trưa, một cột khói mảnh đã đứng lên giữa rừng rễ khổng lồ, và từ khoảnh khắc ấy, hòn đảo thôi là một nơi đi ngang qua để trở thành một nơi người ta quyết định ở lại.

### Year 041 — South Fen rút nước quá sớm

`Primary motion: Ecology` · `Echoes: Economy, Civilization`

Nước ở South Fen năm ấy rút nhanh đến mức bùn chưa kịp mềm đã nứt như mai rùa dưới nắng trắng. Người dân chưa gọi đó là điềm xấu, nhưng những người thu thuế là những người đầu tiên nhận ra rằng mùa tới sẽ không đủ lúa để nuôi cả bờ nam.

### Year 067 — Đêm đèn không tắt ở bến Reedborn

`Primary motion: Storyteller` · `Echoes: Culture, Civilization`

Không ai nhớ chiếc đèn nào được thắp đầu tiên sau mùa cá bội thu, chỉ biết đến nửa đêm thì cả bến cảng đã sáng như mặt nước có sao rơi xuống. Từ năm đó, dân Skyroot thôi coi bến tàu chỉ là nơi buộc thuyền; nó trở thành nơi người ta tụ lại để nhớ rằng mình còn sống sót cùng nhau.

### Year 093 — Những đứa trẻ của cơn gió thứ năm

`Primary motion: Culture` · `Echoes: Myth, Storyteller`

Ở Skyroot, trẻ sinh đúng mùa gió thứ năm bắt đầu không được đặt tên ngay trong ngày đầu tiên nữa. Chúng phải được bế ra mép biển nghe bài hát gọi gió của người già, bởi ai cũng tin linh hồn đến muộn luôn mang theo một món nợ chưa trả với đảo.

---

## Era II – Salt, Grain, and Oaths

### Year 121 — Lời thề muối ở Namar

`Primary motion: Civilization` · `Echoes: Culture, Economy`

Hai thủ lĩnh bờ tây không ký hòa ước bằng đồng hay đá, mà cùng uống nước muối trước mặt dân chúng. Từ ngày đó, ở Namar, một lời hứa được đóng bằng muối bắt đầu nặng hơn mọi con dấu, và cả trật tự thương cảng đổi theo cách con người tin nhau.

### Year 146 — Chim bão chọn một mái nhà

`Primary motion: Myth` · `Echoes: Storyteller, Culture`

Sau khi sét đánh đúng căn nhà của một gia đình vừa sống sót qua mùa bão dữ, dân đảo không gọi đó là trừng phạt. Họ kể rằng Storm Bird chỉ đánh dấu nơi ký ức muốn ở lại, và từ đó những vệt cháy sém trên mái nhà được giữ lại như dấu thánh thay vì bị thay đi.

### Year 173 — Ngũ cốc đi trước binh lính

`Primary motion: Economy` · `Echoes: Civilization, Storyteller`

Trước cả khi hiệp ước thương mại được công bố, những thuyền lúa đầu tiên đã lặng lẽ xuôi Ash River vào vùng biên. Người bán hàng nghe mùi của hòa bình sớm hơn triều đình, và một mùa đói bị đẩy lùi không phải bởi tuyên ngôn, mà bởi những bao hạt đến đúng lúc.

### Year 201 — Lễ Chim Bão trở thành ngày của cả đảo

`Primary motion: Culture` · `Echoes: Myth, Civilization`

Điều bắt đầu như một nghi thức treo lông chim bạc trước cửa nhà đã lớn thành ngày hội chung đầu tiên của Skyroot. Trẻ con được đặt tên mới, thuyền được sơn lại mũi, và ngay cả những người không tin vào chim bão cũng không dám ra khơi khi hòn đảo đang hát cùng một bài.

---

## Era III – Stone, Fire, and Rumor

### Year 244 — Cánh cửa không ai xây

`Primary motion: Creator` · `Echoes: Myth, Storyteller`

Một nhát cuốc của thợ Hael chạm trúng thứ nghe không giống đá ở North Vaults. Khi lớp băng mặn vỡ ra, cả đội đào lùi lại trước một cánh cửa vòm cao quá đầu người, kín những ký hiệu không giống bất cứ triều đại nào còn được nhớ đến, và từ tối đó rượu trong mọi quán trọ phương bắc đều có vị của lời đồn.

### Year 268 — Những xe đá bắt đầu đi về nam

`Primary motion: Economy` · `Echoes: Creator, Civilization`

Các khối đá khai ra từ phương bắc không còn nằm lại trong kho lạnh của Hael, mà bắt đầu xuống xe về phía nam để dựng cầu, cổng, và kho muối. Chẳng ai gọi đó là một bước ngoặt, nhưng đường đi của đá thường báo trước đường đi của quyền lực.

### Year 291 — Ember Choir tìm được giọng của mình

`Primary motion: Myth` · `Echoes: Culture, Storyteller, Economy`

Trong xưởng rèn Hael, bài hát ban đầu chỉ giúp người thợ giữ nhịp búa cho đều. Nhưng chỉ sau một thập kỷ, người ta thôi gọi đó là tiếng lao động; họ gọi nó là tiếng của lửa biết chọn ai được ở gần mình, và cả thành phố bắt đầu lắng nghe lò rèn như lắng nghe đền thờ.

### Year 317 — Dòng tảo xanh phủ kín bến nam

`Primary motion: Ecology` · `Echoes: Economy, Chaos`

Một lớp tảo dày và nhớt phủ lên bến nam của South Fen đúng vào mùa thuyền muối cập bờ. Cá chết nổi theo triền nước, giá muối đổi từng ngày, và lần đầu tiên người ta hiểu rằng một cơn rối loạn lớn không nhất thiết phải bắt đầu bằng gươm hay lửa.

### Year 344 — Không ai giữ cây cầu ở Ash River

`Primary motion: Chaos` · `Echoes: Civilization, Economy, Storyteller`

Cây cầu vẫn còn nguyên vào buổi sáng, nhưng toán lính gác đã biến mất trong đêm mưa tro trước đó. Đến khi mặt trời lên hẳn, thương nhân, người chạy nạn, và lính trinh sát cùng chen trên một lối qua sông, và ai cũng hiểu điều đáng sợ nhất không phải là chiến tranh bắt đầu, mà là chẳng còn ai đủ quyền để ngăn nó nữa.

---

## Era IV – Crowns, Ruin, and Renaming

### Year 379 — Vương miện muối được chấp nhận

`Primary motion: Civilization` · `Echoes: Economy, Culture`

Namar thôi cai trị bằng cân bằng mong manh giữa các gia tộc bến cảng và đặt quyền lực vào một chiếc vương miện duy nhất. Từ ngày ấy, thuế muối không còn là thứ phải thương lượng ở mỗi bến tàu nữa; nó trở thành luật, và luật thì đi xa hơn cả thuyền.

### Year 402 — Thành phố mặc đồ trắng

`Primary motion: Storyteller` · `Echoes: Civilization, Economy`

Leth mở cổng mà không rung chuông chiến, và những người đi vào chỉ mang vải trắng buộc cánh tay cùng bình nước ngọt. Hòa ước ký xong không khiến ai yêu nhau hơn, nhưng ngay sáng hôm sau chợ sông mở lại, và đối với nhiều người, đó là thứ gần nhất với phép màu mà một thành phố có thể làm ra.

### Year 447 — Chợ của những bản đồ chưa vẽ

`Primary motion: Economy` · `Echoes: Creator, Storyteller`

Khi tuyến hải lưu mới ngoài khơi Vey Ash được các thủy thủ Skyroot học thuộc, bến cảng phía đông bỗng đầy lên những tấm da, mảnh gỗ, và bản đồ dở dang bán với giá ngang muối tốt. Asterra bắt đầu không chỉ mua bán hàng hóa, mà mua bán cả những nơi chưa ai thực sự đặt chân đến.

### Year 511 — Ngôi sao đuôi lửa trên Glass Bay

`Primary motion: Myth` · `Echoes: Chaos, Storyteller`

Một vệt sáng xanh cắt ngang trời đúng tuần ba thuyền cá mất tích ngoài vịnh. Trong vòng một năm, trẻ con ven biển đã được dạy rằng sao đuôi lửa luôn đòi một cái tên trước khi chịu rời đi, và mọi vụ mất tích sau đó đều thôi là tai nạn để trở thành một cuộc gọi chưa trả lời.

### Year 563 — Hàng xe đi về phía tây

`Primary motion: Civilization` · `Echoes: Ecology, Economy`

Hàng trăm gia đình rời vùng bùn nứt của South Fen bằng xe gỗ bọc vải đen, kéo nhau về phía đồng cỏ cao phía tây. Dấu bánh xe của họ về sau thành con đường thương lộ đầu tiên của cả vùng, như thể chính nỗi tuyệt vọng đã mở một tuyến mạch máu mới cho thế giới.

### Year 640 — Lá cờ cuối cùng của Orun rơi xuống

`Primary motion: Chaos` · `Echoes: Civilization, Storyteller`

Buổi chiều lá cờ xanh-đen cuối cùng của Orun bị hạ xuống, chẳng có ai reo mừng và cũng chẳng có lễ đăng quang nào diễn ra ngay sau đó. Chỉ trong một mùa, những pháo đài từng giữ biên giới của cả đế chế đã thành trạm thu phí cho lãnh chúa nhỏ, và cái tên Orun bắt đầu rời khỏi miệng người sống để đi vào giọng kể của người già.

### Year 703 — Con cái của gỗ thủy triều

`Primary motion: Storyteller` · `Echoes: Culture, Civilization, Myth`

Thế hệ sinh ra sau chiến tranh trên Skyroot không muốn mang tên của cha ông nữa; họ tự gọi mình là con cái của Tidewood, như thể đau thương chỉ chịu yên nếu được đổi tên trước. Triều đình mới hiểu rất nhanh sức mạnh của một cái tên đẹp, và từ đó cả một kỷ nguyên được mở ra bằng ngôn ngữ trước khi được mở ra bằng luật.

---

## Why This Feels Polyphonic

Bộ card này không đi theo một giọng nói duy nhất.

- `Creator` mở rộng mặt bằng và khởi tạo ấn tượng về world scale.
- `Civilization` đưa vào luật, ngai vị, thỏa ước, và biểu tượng quyền lực.
- `Storyteller` đưa vào nhịp sống, ký ức chung, và những khoảnh khắc con người nhìn lại nhau.
- `Culture` tạo nghi lễ, tên gọi, và những thói quen thành bản sắc.
- `Myth` phủ nghĩa thiêng lên những gì con người không giải thích hết.
- `Ecology` đổi nhịp sống bằng nước, gió, mùa, và bệnh của đất.
- `Economy` cho thấy quyền lực của đường đi, giá cả, và sự phụ thuộc.
- `Chaos` cắt đứt những gì tưởng đã ổn định.

Trong khi đó:

- `Guardian` giữ cho tất cả vẫn hợp logic.
- `Historian` biến dòng chảy đó thành canon để `Dream Feed` đọc được và `Timeline` dùng được.

Nếu chỉ có `Historian` lộ ra ở bề mặt, feed sẽ biến thành niên biểu. Nếu chỉ có `Storyteller` lộ ra ở bề mặt, feed sẽ thành prose đẹp nhưng mất cảm giác đây là một thế giới được mô phỏng. Polyphony nằm ở chỗ người đọc vừa cảm được câu chuyện, vừa cảm được các lực tạo world đang kéo nhau bên dưới.

---

## Implementation Notes

Nếu muốn đưa bộ này vào UI hoặc fixture, mỗi card có thể map thành:

- `year`
- `title`
- `summary`
- `event_type`
- `primary_agent`
- `echo_agents`
- `tags`
- `linked_regions`
- `linked_civilizations`
- `is_canonical`

Bộ sample này nên được đọc cùng với:

- `DREAM-FEED-COPY-RUBRIC.md`
- `ui-concepts.md`
- `agent-specs/historian.md`

Nếu cần bước tiếp theo, tài liệu này có thể được chuyển tiếp thành:

- `JSON fixtures` cho API/UI
- `prompt templates` cho multi-agent generation
- `eval cases` để chấm xem một card có đủ polyphonic hay vẫn đang khô như timeline
