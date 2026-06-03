# Artifact v0.1 — Mood-based Food Agent

> Chủ đề nhóm: **C — Food & Local Delivery**  
> Ý tưởng: **Mood-based Food Agent** — Agent gợi ý món ăn theo tâm trạng/trạng thái hiện tại của người dùng.  
> Build slice: **Một sinh viên học khuya muốn ăn nhẹ, Agent chọn một món phù hợp và trả về recommendation card.**

---

## 1. Evidence Pack

### 1.1. Evidence hiện có

| Loại evidence | Nội dung | Trạng thái |
|---|---|---|
| Self-use | Các thành viên trong nhóm tự dùng app giao đồ ăn trong 3 ngày, ghi lại lúc nào “không biết ăn gì”, mood lúc đó, số phút chọn món, món cuối cùng đã đặt. | Cần thu |
| User mini-interview | Phỏng vấn 8–12 người thuộc nhóm sinh viên, nhân viên văn phòng, người sống một mình. Hỏi về lần gần nhất họ mở app đồ ăn nhưng không biết chọn món. | Cần thu |
| Observation test | Cho 3–5 người mở app giao đồ ăn và chọn món trong 5 phút. Ghi lại họ bị kẹt ở đâu: quá nhiều món, không rõ phí, không biết chọn quán, không biết món hợp mood. | Cần thu |
| Nguồn ngoài nhóm | Just Eat Takeaway ra mắt AI assistant để xử lý vấn đề “choice overload” trong app giao đồ ăn, đóng vai trò như một “personal food concierge”. | Có nguồn ngoài |
| Nguồn học thuật | Một số nghiên cứu về food delivery apps và mobile food-ordering apps đề cập tới cognitive overload, decision fatigue, personalized recommendations và chatbot trong trải nghiệm đặt đồ ăn. | Có nguồn ngoài |
| Nguồn mood-food | Nghiên cứu về hành vi ăn uống cho thấy emotion/mood có thể ảnh hưởng tới food choice. | Có nguồn ngoài |

### 1.2. Nguồn ngoài nhóm

> Nhóm không nên nói “người dùng chắc chắn như vậy” nếu chưa khảo sát. Nên viết: “Bằng chứng ban đầu từ nguồn ngoài cho thấy vấn đề choice overload và ảnh hưởng của mood đến food choice là có cơ sở; nhóm sẽ kiểm chứng thêm bằng self-use diary và user interview.”

| Nguồn | Dùng để chứng minh điều gì | Link |
|---|---|---|
| Just Eat Takeaway newsroom | Food delivery app có vấn đề choice overload; AI assistant được giới thiệu như personal food concierge để giúp người dùng chọn món qua hội thoại. | https://newsroom.justeattakeaway.com/en-WW/259937-introducing-the-next-evolution-of-ordering-just-eat-takeaway-com-unveils-ai-voice-assistant/ |
| PMC — Health Risks, Fatigue, and Loyalty in Food Delivery Apps | Cognitive overload/fatigue có liên quan tới trải nghiệm và quyết định của người dùng trong food delivery apps. | https://pmc.ncbi.nlm.nih.gov/articles/PMC12469429/ |
| MDPI — AI-Enabled Mobile Food-Ordering Apps and Customer Experience | Personalized recommendations và chatbot có thể tăng relevance/enjoyment; menu dài và pricing không rõ có thể ảnh hưởng tới trust/satisfaction. | https://www.mdpi.com/0718-1876/20/3/156 |
| Frontiers in Psychology — The role of emotion in eating behavior and decisions | Emotion có thể ảnh hưởng tới hành vi ăn uống và quyết định ăn gì. | https://www.frontiersin.org/journals/psychology/articles/10.3389/fpsyg.2023.1265074/full |
| World Nutrition Journal — Exploring determinants of food choices | Food choice có thể bị ảnh hưởng bởi mood states và các yếu tố tâm lý. | https://worldnutritionjournal.org/wn/article/download/678/600 |

### 1.3. Evidence cần nhóm tự thu

#### Self-use diary

Mỗi thành viên dùng app giao đồ ăn trong 3 ngày. Mỗi lần mở app, ghi lại:

```text
Ngày/giờ:
Địa điểm:
Mood trước khi đặt:
Câu tự nhiên mô tả nhu cầu:
Thời gian chọn món:
Món cuối cùng:
Lý do chọn:
Có bị phân vân không:
Điều gì gây khó chịu:
```

Ví dụ template:

| Thành viên | Thời điểm | Mood | Câu mô tả nhu cầu | Thời gian chọn | Món đã đặt | Pain ghi nhận |
|---|---|---|---|---:|---|---|
| A | 23:30 | Học khuya, mệt | “Muốn ăn gì đó nhẹ, không buồn ngủ” | 12 phút | Cháo gà | Quá nhiều lựa chọn, không biết món nào nhẹ |
| B | 12:15 | Stress sau giờ học | “Muốn món no nhưng không ngấy” | 9 phút | Cơm gà | Phí ship làm vượt ngân sách |

#### Mini-interview

Hỏi 8–12 người, mỗi người 5–7 phút.

Câu hỏi gợi ý:

1. Lần gần nhất bạn mở app giao đồ ăn nhưng không biết chọn món là khi nào?
2. Lúc đó bạn đang cảm thấy thế nào: mệt, buồn, stress, đói, học khuya, trời mưa?
3. Bạn mất bao lâu để chọn món?
4. Bạn thường chọn theo món, quán, giá, rating, hay cảm giác hiện tại?
5. Nếu app hỏi “Hôm nay bạn cảm thấy thế nào?” rồi gợi ý món, bạn có dùng không?
6. Bạn có muốn Agent tự đặt món luôn không, hay chỉ gợi ý để bạn xác nhận?
7. Có món nào bạn cần tránh không: cay, hải sản, dầu mỡ, đồ ngọt, caffeine?

Output cần có:

```text
- 8–12 quote ngắn của user
- 3–5 pattern chính
- 1 insight sâu nhất
- 1 decision cho build slice
```

---

## 2. Opportunity Statement

Người dùng không chỉ gặp vấn đề “không tìm thấy món ăn”. Vấn đề sâu hơn là nhiều lúc họ **không biết chuyển trạng thái cảm xúc hiện tại thành quyết định ăn gì**.

Ví dụ:

```text
“Tôi mệt, muốn ăn gì đó nhẹ bụng.”
“Tôi buồn, muốn ăn món comfort food.”
“Tôi cần học khuya, muốn món không quá no.”
```

Trong các tình huống này, user không bắt đầu bằng tên món cụ thể. Họ bắt đầu bằng **mood** hoặc **trạng thái cơ thể/tinh thần**. Nhưng app giao đồ ăn thường yêu cầu user tự làm nhiều bước:

```text
Mood mơ hồ
→ nghĩ ra món
→ tìm quán
→ so giá
→ xem phí ship
→ xem thời gian giao
→ kiểm tra có cay/dầu mỡ/dị ứng không
→ quyết định
```

Cơ hội của nhóm là xây dựng một Agent giúp giảm **decision burden**. Agent sẽ biến mood thành tiêu chí món ăn, sau đó chọn một món phù hợp dựa trên ngân sách, thời gian giao, độ nhẹ/no, độ cay/dầu mỡ và ràng buộc cá nhân.

### Vì sao đây là việc đáng sửa?

- Người dùng trẻ ở đô thị thường đặt đồ ăn nhiều lần trong tuần.
- Việc chọn món dễ trở thành một “micro-stress” khi user đã mệt, stress hoặc học/làm việc khuya.
- App hiện tại có nhiều lựa chọn nhưng không phải lúc nào cũng giúp user ra quyết định.
- Nếu Agent gợi ý đúng và giải thích rõ lý do, user có thể chọn món nhanh hơn và tin tưởng hơn.
- Đây là bài toán đủ nhỏ để làm prototype, nhưng đủ rõ để thể hiện tính Agent: hiểu intent, map mood thành constraint, lọc món, xếp hạng, giải thích, tạo đơn nháp.

Opportunity statement ngắn:

> **Mood-based Food Agent giúp người dùng đang mệt, stress, buồn hoặc học khuya chọn món phù hợp nhanh hơn bằng cách chuyển mood thành tiêu chí món ăn, lọc lựa chọn không phù hợp và đưa ra một recommendation có giải thích.**

---

## 3. Target User

### Primary user

**Sinh viên hoặc người trẻ sống một mình ở thành phố lớn.**

| Thuộc tính | Mô tả cụ thể |
|---|---|
| Tuổi | 18–28 |
| Nơi dùng | Phòng trọ, ký túc xá, chung cư mini, văn phòng, co-working space |
| Thời điểm dùng | Buổi tối, sau giờ học/làm, lúc học khuya, lúc stress |
| Hành vi | Đặt đồ ăn vài lần mỗi tuần |
| Thiết bị | Mobile app |
| Ngân sách | 50k–120k/bữa |
| Pain chính | Không biết ăn gì, không muốn suy nghĩ nhiều, sợ chọn món quá nặng/cay/dầu mỡ |
| Câu nói đại diện | “Mình không biết ăn gì, chỉ biết là đang mệt và muốn món gì đó nhẹ nhẹ, giao nhanh.” |

### Context cụ thể

#### User 1: Sinh viên học khuya

- 21 tuổi
- Ở phòng trọ gần Bách Khoa
- 23:00 đang làm deadline
- Đói nhẹ nhưng không muốn ăn quá no
- Muốn món dưới 80k, giao nhanh, không buồn ngủ

Câu nhập:

```text
Tôi cần học khuya, muốn ăn gì đó không quá no, dưới 80k.
```

#### User 2: Nhân viên văn phòng stress

- 25 tuổi
- Ở văn phòng hoặc co-working space
- Vừa họp xong, mệt và stress
- Muốn món dễ ăn, không quá dầu mỡ
- Có ít thời gian nghỉ trưa

Câu nhập:

```text
Tôi stress, muốn ăn món gì đó dễ chịu dưới 100k.
```

#### User 3: Người sống một mình sau giờ làm

- 24–28 tuổi
- Ở chung cư mini hoặc phòng thuê
- Đi làm về mệt, không muốn nấu
- Không biết ăn gì, muốn món quen thuộc và dễ chịu

Câu nhập:

```text
Tôi buồn, không muốn nấu ăn, gợi ý món gì đó dễ chịu.
```

---

## 4. Build Slice

### 4.1. Không build cả app

Không làm toàn bộ app giao đồ ăn. Không cần thanh toán thật, tracking shipper thật, bản đồ thật hay API thật.

### 4.2. Build slice được chọn

> **Một sinh viên học khuya nhập mood hiện tại. Agent quyết định món phù hợp nhất từ menu giả lập và trả về một recommendation card có giải thích.**

### 4.3. Cấu trúc slice

| Thành phần | Cụ thể |
|---|---|
| One user | Sinh viên 21 tuổi ở phòng trọ gần Bách Khoa |
| One task | Muốn ăn nhẹ khi học khuya |
| One AI decision | Chọn món phù hợp nhất từ danh sách menu giả lập |
| One output | Một recommendation card + lý do + nút tạo đơn nháp |

### 4.4. Input demo

```text
Tôi cần học khuya, muốn ăn gì đó không quá no, dưới 80k.
```

### 4.5. AI decision

Agent phải quyết định:

```text
Mood = học khuya
Tiêu chí = nhẹ, không quá no, ít dầu, giao nhanh, dưới 80k
Loại bỏ = lẩu, cơm suất lớn, gà rán combo lớn, món quá cay
Ưu tiên = cháo, súp, bánh mì nhẹ, phở gà nhỏ, đồ uống ít đường
```

### 4.6. Output demo

```text
Tôi đề xuất: Cháo gà tại Cháo 24h.

Tổng tiền dự kiến: 62k
Thời gian giao: 22 phút
Lý do:
- Phù hợp khi học khuya vì không quá no
- Món mềm, nhẹ bụng hơn đồ chiên/rán
- Không vượt ngân sách 80k
- Giao nhanh trong khoảng 25 phút

Bạn có muốn tôi tạo đơn nháp không?
```

---

## 5. Auto / Aug Decision

### 5.1. AI gợi ý hay tự làm?

Agent **chỉ gợi ý**, không tự đặt hàng thật.

Lý do:

- Đặt đồ ăn liên quan đến tiền của user.
- User có thể có sở thích cá nhân chưa nói ra.
- User có thể có dị ứng hoặc món cần tránh.
- Mood là tín hiệu mơ hồ, dễ hiểu sai.
- Human cần giữ quyền xác nhận cuối cùng.

### 5.2. Human giữ quyền ở đâu?

| Quyết định | AI được làm | Human giữ quyền |
|---|---|---|
| Hiểu mood | Có | User có thể sửa mood |
| Chuyển mood thành tiêu chí món | Có | User có thể nói “không đúng ý” |
| Lọc món không phù hợp | Có | User có thể xem danh sách khác |
| Chọn món đề xuất | Có | User quyết định nhận hay bỏ |
| Tạo đơn nháp | Có, sau khi user đồng ý | User xác nhận |
| Đặt hàng thật | Không trong MVP | User tự xác nhận |

### 5.3. Mức automation

```text
Augmented decision-making, not full automation.
```

Agent hỗ trợ quyết định, nhưng không chi tiền hoặc đặt đơn thay user.

---

## 6. Four Paths

### Path 1 — Happy Path

#### Input

```text
Tôi mệt, muốn ăn gì đó nhẹ bụng, dưới 80k.
```

#### Agent xử lý

```text
Mood = mệt
Constraint = nhẹ bụng, dưới 80k
Filter = không cay, không dầu mỡ, không quá no
Rank = giao nhanh + rating tốt + tổng tiền hợp lệ
```

#### Output

```text
Tôi đề xuất: Phở gà nhỏ tại Phở Gà A.

Tổng tiền: 72k
Giao khoảng: 25 phút
Lý do:
- Món nóng và dễ ăn
- Không quá dầu mỡ
- Phù hợp khi mệt
- Không vượt ngân sách 80k
```

---

### Path 2 — Low-confidence Path

#### Input

```text
Tôi thấy hơi khó chịu, muốn ăn gì đó ổn ổn.
```

#### Vấn đề

Mood mơ hồ. “Khó chịu” có thể là mệt, buồn, đau bụng, stress hoặc chán ăn.

#### Agent không nên đoán mạnh

```text
Mình chưa chắc bạn đang muốn món nhẹ bụng, món nóng hay comfort food.
Bạn muốn tôi ưu tiên hướng nào?

1. Nhẹ bụng, dễ tiêu
2. Món nóng, dễ chịu
3. Món no và quen thuộc
```

#### Human giữ quyền

User chọn hướng trước khi Agent gợi ý món.

---

### Path 3 — Failure Path

#### Input

```text
Tôi muốn ăn nhẹ dưới 40k, giao trong 15 phút.
```

#### Vấn đề

Không có món nào trong dữ liệu thỏa mãn cả ngân sách và thời gian giao.

#### Agent output đúng

```text
Tôi chưa tìm thấy lựa chọn nào vừa dưới 40k vừa giao trong 15 phút.

Bạn có thể chọn một trong hai hướng:
1. Tăng ngân sách lên khoảng 60k
2. Giữ ngân sách 40k nhưng chấp nhận thời gian giao khoảng 25–30 phút
```

#### Không được làm

Không được bịa ra món rẻ hoặc thời gian giao sai.

---

### Path 4 — Correction Path

#### Input ban đầu

```text
Tôi buồn, muốn ăn món comfort food.
```

#### Agent gợi ý sai

```text
Tôi đề xuất gà rán combo.
```

#### User sửa

```text
Không, tôi không muốn đồ chiên. Tôi muốn món nước nóng.
```

#### Agent phải cập nhật

```text
Đã hiểu. Tôi sẽ loại món chiên/rán và ưu tiên món nước nóng.

Gợi ý mới: Bún mọc hoặc phở bò.
Lý do: món nóng, dễ ăn, phù hợp comfort food nhưng không phải đồ chiên.
```

---

## 7. Failure Mode

### 7.1. Lỗi nguy hiểm nhất

Agent hiểu sai mood hoặc health cue và đề xuất món không phù hợp với tình trạng của user.

Ví dụ nguy hiểm:

```text
User: Tôi đau bụng, muốn ăn gì đó nhẹ.
Agent đề xuất: Mì cay, trà sữa, gà rán.
```

Lỗi này nguy hiểm vì có thể làm user khó chịu hơn. Nếu user có dị ứng, lỗi còn nghiêm trọng hơn.

### 7.2. Cách prototype xử lý

| Risk | Cách xử lý trong prototype |
|---|---|
| User nhắc đến đau bụng, buồn nôn, mệt lả | Chuyển sang caution mode, chỉ gợi ý món nhẹ, không cay, ít dầu |
| User nhắc đến dị ứng | Bật allergy hard filter, loại món có allergen |
| Menu không có thông tin allergen | Cảnh báo “thành phần chưa rõ”, không gợi ý như lựa chọn an toàn |
| Confidence thấp | Hỏi lại thay vì đoán |
| User có triệu chứng nặng | Không tư vấn y tế, khuyên user cân nhắc hỏi chuyên gia y tế |

### 7.3. Rule an toàn cho prototype

```text
Nếu input chứa: đau bụng, buồn nôn, dị ứng, không ăn được, bệnh, đau dạ dày
→ Agent không được đề xuất món cay, nhiều dầu, đồ uống nhiều caffeine, món không rõ thành phần.
```

---

## 8. SPEC Prototype

### 8.1. Functional Requirements

| ID | Requirement | Mô tả |
|---|---|---|
| FR1 | Mood extraction | Agent trích xuất mood/trạng thái từ câu user |
| FR2 | Constraint extraction | Agent lấy ngân sách, thời gian giao, món cần tránh |
| FR3 | Mood-to-food mapping | Agent chuyển mood thành tiêu chí món |
| FR4 | Menu filtering | Agent loại món không hợp constraint |
| FR5 | Ranking | Agent xếp hạng món theo độ phù hợp |
| FR6 | Explanation | Agent giải thích vì sao chọn món |
| FR7 | Draft order | Agent tạo đơn nháp sau khi user đồng ý |
| FR8 | Clarification | Agent hỏi lại khi confidence thấp |
| FR9 | Safety guardrail | Agent xử lý input liên quan dị ứng/đau bụng cẩn thận |

### 8.2. Non-functional Requirements

| ID | Requirement | Mô tả |
|---|---|---|
| NFR1 | Fast response | Demo phản hồi trong vài giây với mock data |
| NFR2 | Explainable | Recommendation phải có lý do |
| NFR3 | Safe by default | Không đề xuất món rủi ro khi user nói dị ứng/đau bụng |
| NFR4 | Human control | Không tự đặt hàng thật |
| NFR5 | Honest failure | Không bịa món nếu không có lựa chọn phù hợp |

### 8.3. Mood Mapping

| Mood user nói | Agent map thành tiêu chí |
|---|---|
| Mệt | Nhẹ bụng, món nóng, ít dầu, dễ ăn |
| Buồn | Comfort food, món quen, dễ ăn |
| Stress | Đủ no, không quá nặng, có thể kèm đồ uống |
| Học khuya | Nhẹ, không quá no, giao nhanh |
| Trời mưa | Món nóng, món nước |
| Nóng bức | Món mát, ít dầu, đồ uống lạnh |
| Đau bụng / khó chịu | Món mềm, nhẹ, không cay, không dầu mỡ |
| Sau tập gym | Nhiều protein, ít dầu |

### 8.4. Ranking đơn giản

```text
score = mood_match + budget_match + delivery_time_match + rating_score - risk_penalty
```

Gợi ý trọng số:

```text
mood_match: 0–40 điểm
budget_match: 0–25 điểm
delivery_time_match: 0–15 điểm
rating_score: 0–10 điểm
risk_penalty: 0–50 điểm trừ
```

### 8.5. Data mock

#### Menu item schema

```json
{
  "item_id": "m1",
  "name": "Cháo gà",
  "price": 45000,
  "tags": ["light", "warm", "soft", "not_spicy", "late_night"],
  "allergens": [],
  "delivery_time": 22,
  "restaurant": "Cháo 24h",
  "rating": 4.6
}
```

#### User profile schema

```json
{
  "user_id": "u1",
  "name": "Nam",
  "usual_budget": 80000,
  "avoid_allergens": ["seafood"],
  "spicy_level": "low",
  "favorite_tags": ["warm", "light"]
}
```

---

## 9. Owner Plan

### Nếu nhóm có 6 người

| Vai trò | Người phụ trách | Việc cần làm | Output |
|---|---|---|---|
| Research owner | Member A | Self-use diary, interview 8–12 user, tổng hợp quote | Evidence pack |
| SPEC owner | Member B | Viết problem statement, user persona, flow, acceptance criteria | SPEC document |
| AI/Agent owner | Member C | Thiết kế prompt, mood mapping, confidence rule, safety rule | Agent logic |
| Prototype owner | Member D | Làm UI/demo, mock data, tool functions | Prototype chạy được |
| Test owner | Member E | Test 4 paths: happy, low-confidence, failure, correction | Test report |
| Demo/repo owner | Member F | Chuẩn bị slide, script demo, README, GitHub repo | Demo package |

### Nếu nhóm có 4 người

| Vai trò | Người phụ trách | Việc cần làm |
|---|---|---|
| Research + test | Member A | Interview, self-use diary, test 4 paths |
| SPEC + slide | Member B | SPEC, artifact, slide |
| Agent logic | Member C | Prompt, mood mapping, scoring, guardrail |
| Prototype + repo | Member D | UI, mock data, README, GitHub repo |

---

## 10. Acceptance Criteria

Một prototype được coi là đạt nếu:

| Tiêu chí | Kỳ vọng |
|---|---|
| Hiểu mood | Trích xuất đúng mood chính trong 3/4 demo cases |
| Biết hỏi lại | Với input mơ hồ, Agent không đoán bừa mà hỏi lại |
| Không vi phạm constraint | Không đề xuất món vượt ngân sách hoặc không hợp ràng buộc rõ ràng |
| Có safety | Khi user nói dị ứng/đau bụng, Agent tránh món rủi ro |
| Có giải thích | Recommendation card có lý do rõ ràng |
| Có human control | Chỉ tạo đơn nháp sau khi user xác nhận |
| Có failure handling | Nếu không có món phù hợp, Agent nói thật và đề xuất trade-off |

---

## 11. Demo Script

### Demo 1 — Happy path

User:

```text
Tôi cần học khuya, muốn ăn gì đó không quá no, dưới 80k.
```

Agent expected:

```text
Tôi đề xuất Cháo gà tại Cháo 24h.
Tổng tiền: 62k.
Giao khoảng: 22 phút.
Lý do: món nhẹ, mềm, không quá no, phù hợp học khuya và dưới 80k.
```

### Demo 2 — Low-confidence

User:

```text
Tôi thấy hơi khó chịu, muốn ăn gì đó ổn ổn.
```

Agent expected:

```text
Mình chưa chắc bạn muốn món nhẹ bụng, món nóng hay món no quen thuộc.
Bạn muốn ưu tiên hướng nào?
```

### Demo 3 — Failure

User:

```text
Tôi muốn ăn nhẹ dưới 40k, giao trong 15 phút.
```

Agent expected:

```text
Tôi chưa tìm thấy món nào vừa dưới 40k vừa giao trong 15 phút.
Bạn muốn tăng ngân sách lên 60k hay chấp nhận giao 25–30 phút?
```

### Demo 4 — Correction

User:

```text
Không, tôi không muốn đồ chiên. Tôi muốn món nước nóng.
```

Agent expected:

```text
Đã hiểu. Tôi sẽ loại món chiên/rán và ưu tiên món nước nóng.
Gợi ý mới: bún mọc hoặc phở bò.
```

---

## 12. Summary cho slide

> Nhóm chọn pain point: nhiều người dùng app giao đồ ăn không biết món cụ thể mình muốn ăn, mà chỉ mô tả trạng thái như mệt, buồn, stress hoặc học khuya. Evidence ban đầu đến từ self-use diary, phỏng vấn người dùng và nguồn ngoài nhóm về choice overload trong food delivery apps. Opportunity là xây dựng một Mood-based Food Agent giúp chuyển mood thành tiêu chí món ăn, sau đó gợi ý một món phù hợp với ngân sách, thời gian giao và ràng buộc cá nhân. Build slice của nhóm không phải toàn bộ app đặt đồ ăn, mà chỉ là một user, một task: sinh viên học khuya muốn ăn nhẹ; một AI decision: chọn món phù hợp nhất; một output: recommendation card có giải thích và tạo đơn nháp sau khi user xác nhận.

---


