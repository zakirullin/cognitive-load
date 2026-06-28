# Cognitive load mới là thứ quan trọng

[Agents](https://github.com/zakirullin/cognitive-load/blob/main/README.agents.md) | [Blog version](https://minds.md/zakirullin/cognitive) | [Chinese](https://github.com/zakirullin/cognitive-load/blob/main/README.zh-cn.md) | [Korean](README.ko.md) | [Turkish](README.tr.md) | [Japanese](README.ja.md) | [Vietnamese](README.vi.md)

*Đây là tài liệu sống, cập nhật lần cuối: **Tháng 10/2025.** Mọi đóng góp đều được chào đón!*

## Giới thiệu
Có quá nhiều buzzword và best practice ngoài kia, nhưng phần lớn đều thất bại. Chúng thất bại vì chúng được tưởng tượng ra, không phải thực tế. Những ý tưởng này dựa trên thẩm mỹ và đánh giá chủ quan. Chúng ta cần thứ gì đó fundamental hơn, thứ không thể sai được.

Đôi khi chúng ta cảm thấy bối rối khi đọc code. Sự bối rối tốn thời gian và tiền bạc. Sự bối rối được gây ra bởi *cognitive load* cao. Đây không phải một khái niệm trừu tượng fancy, mà là **một giới hạn cơ bản của con người.** Nó không phải tưởng tượng, nó ở đó và chúng ta cảm nhận được.

Vì chúng ta dành nhiều thời gian đọc và hiểu code hơn là viết nó, chúng ta nên liên tục tự hỏi liệu mình có đang nhét quá nhiều cognitive load vào code hay không.

## Cognitive load
> Cognitive load là lượng suy nghĩ mà một developer cần để hoàn thành một task.

Khi đọc code, bạn đưa các thứ như giá trị biến, control flow logic và call sequence vào đầu. Một người bình thường có thể giữ khoảng [bốn chunk như vậy](https://github.com/zakirullin/cognitive-load/issues/16) trong working memory. Khi cognitive load đạt ngưỡng này, việc hiểu trở nên khó khăn hơn nhiều.

*Giả sử chúng ta được yêu cầu fix bug cho một project hoàn toàn xa lạ. Người ta nói có một developer thông minh đã contribute vào đó. Nhiều kiến trúc xịn, library fancy và công nghệ trendy được sử dụng. Nói cách khác, **tác giả đã tạo ra cognitive load cao cho chúng ta.***

<div align="center">
  <img src="/img/cognitiveloadv6.png" alt="Cognitive load" width="750">
</div>

Chúng ta nên giảm cognitive load trong project càng nhiều càng tốt.

<details>
  <summary><b>Cognitive load và interruption</b></summary>
  <div align="center">
    <img src="img/interruption.jpeg" width="480">
  </div>
</details>

> Chúng ta sẽ dùng "cognitive load" theo nghĩa informal; đôi khi nó khớp với khái niệm khoa học về Cognitive Load, nhưng chúng ta không biết chính xác chỗ nào khớp và chỗ nào không.

## Các loại cognitive load
**Intrinsic** - do độ khó vốn có của task gây ra. Không thể giảm được, nó nằm trong bản chất của software development.

**Extraneous** - do cách trình bày thông tin tạo ra. Do các yếu tố không liên quan trực tiếp đến task, như thói quen của tác giả thông minh. Có thể giảm đáng kể. Chúng ta sẽ tập trung vào loại cognitive load này.

<div align="center">
  <img src="/img/smartauthorv14thanksmari.png" alt="Intrinsic vs Extraneous" width="600">
</div>

Cùng nhảy thẳng vào các ví dụ thực tế cụ thể về extraneous cognitive load.

---

Chúng ta sẽ gọi level của cognitive load như sau:
`🧠`: working memory trong lành, zero cognitive load
`🧠++`: hai fact trong working memory, cognitive load tăng
`🤯`: cognitive overload, hơn 4 fact

> Não bộ chúng ta phức tạp và chưa được khám phá nhiều hơn thế, nhưng ta có thể dùng model đơn giản này.

## Conditional phức tạp
```go
if val > someConstant // 🧠+
    && (condition2 || condition3) // 🧠+++, prev cond phải true, một trong c2 hoặc c3 phải true
    && (condition4 && !condition5) { // 🤯, tới đây ta đã rối
    ...
}
```

Đưa vào các biến trung gian với tên có nghĩa:
```go
isValid = val > someConstant
isAllowed = condition2 || condition3
isSecure = condition4 && !condition5
// 🧠, không cần nhớ các condition, có biến mô tả rồi
if isValid && isAllowed && isSecure {
    ...
}
```

## Nested if
```go
if isValid { // 🧠+, okay code nested chỉ apply cho valid input
    if isSecure { // 🧠++, ta chỉ làm stuff cho valid và secure input
        stuff // 🧠+++
    }
}
```

So sánh với early return:
```go
if !isValid
    return

if !isSecure
    return

// 🧠, ta không quan tâm early return ở trên, nếu tới đây thì mọi thứ OK

stuff // 🧠+
```

Ta có thể focus vào happy path thôi, giải phóng working memory khỏi các precondition.

## Ác mộng kế thừa
Ta được yêu cầu thay đổi vài thứ cho admin user: `🧠`

`AdminController extends UserController extends GuestController extends BaseController`

Ồ, một phần functionality nằm trong `BaseController`, coi thử: `🧠+`
Role mechanic cơ bản được giới thiệu trong `GuestController`: `🧠++`
Mọi thứ được thay đổi một phần trong `UserController`: `🧠+++`
Cuối cùng tới đây, `AdminController`, code thôi! `🧠++++`

À đợi, còn có `SuperuserController` extend `AdminController`. Nếu sửa `AdminController` ta có thể làm hỏng class kế thừa, nên xem `SuperuserController` trước: `🤯`

Ưu tiên composition hơn inheritance. Ta sẽ không đi sâu - có [rất nhiều tài liệu](https://www.youtube.com/watch?v=hxGOiiR9ZKg) về việc này.

## Quá nhiều method, class hoặc module nhỏ
> Method, class và module có thể thay thế cho nhau trong context này.

Các mantra kiểu "method nên ngắn hơn 15 dòng code" hay "class nên nhỏ" hóa ra hơi sai.

**Deep module** - interface đơn giản, functionality phức tạp
**Shallow module** - interface tương đối phức tạp so với functionality nhỏ mà nó cung cấp

<div align="center">
  <img src="/img/deepmodulev8.png" alt="Deep module" width="700">
</div>

Có quá nhiều shallow module có thể gây khó khăn cho việc hiểu project. **Không chỉ phải nhớ responsibility của từng module, mà còn phải nhớ tất cả interaction giữa chúng.** Để hiểu mục đích của shallow module, trước tiên ta phải xem functionality của các module liên quan. Nhảy giữa các component shallow như vậy rất mệt mỏi về mặt tinh thần, <a target="_blank" href="https://blog.separateconcerns.com/2023-09-11-linear-code.html">linear thinking</a> tự nhiên hơn với con người.

> Information hiding là tối quan trọng, và ta không ẩn được nhiều complexity trong shallow module.

Tôi có hai pet project, cả hai đều khoảng 5K dòng code. Project đầu có 80 shallow class, trong khi project thứ hai chỉ có 7 deep class. Tôi không maintain hai project này trong một năm rưỡi.

Khi quay lại, tôi nhận ra rằng cực kỳ khó để tách rõ tất cả interaction giữa 80 class trong project đầu. Tôi phải rebuild một lượng cognitive load khổng lồ trước khi có thể bắt đầu code. Mặt khác, tôi có thể nắm bắt project thứ hai nhanh chóng vì nó chỉ có vài deep class với interface đơn giản.

> Component tốt nhất là những component cung cấp functionality mạnh mẽ nhưng có interface đơn giản.
>
> *John Ousterhout, A Philosophy of Software Design*

Interface của Unix I/O rất đơn giản. Nó chỉ có năm basic call:
```python
open(path, flags, permissions)
read(fd, buffer, count)
write(fd, buffer, count)
lseek(fd, offset, referencePosition)
close(fd)
```

Implementation hiện đại của interface này có **hàng trăm nghìn dòng code.** Rất nhiều complexity được ẩn bên dưới. Nhưng nó dễ dùng nhờ interface đơn giản.

> Ví dụ deep module này được lấy từ sách [A Philosophy of Software Design](https://web.stanford.edu/~ouster/cgi-bin/book.php) của John Ousterhout. Không chỉ cuốn sách này bàn về bản chất của complexity trong software development, mà còn có cách giải thích hay nhất về paper có ảnh hưởng của Parnas [On the Criteria To Be Used in Decomposing Systems into Modules](https://www.win.tue.nl/~wstomv/edu/2ip30/references/criteria_for_modularization.pdf). Cả hai đều là tài liệu bắt buộc phải đọc. Các tài liệu liên quan khác: [A Philosophy of Software Design vs Clean Code](https://github.com/johnousterhout/aposd-vs-clean-code), [It's probably time to stop recommending Clean Code](https://qntm.org/clean), [Small Functions considered Harmful](https://copyconstruct.medium.com/small-functions-considered-harmful-91035d316c29).

<details>
    <summary><b>Những thứ quan trọng nên to, ví dụ</b></summary>
    <br>
    <div align="center">
        <img src="/img/dirty.png" alt="Clean vs Dirty" width="600">
    </div>
    <blockquote>Nếu bạn cho phép các function "crux" quan trọng to hơn ("dirty"), sẽ dễ dàng hơn để pick chúng ra khỏi biển function, chúng rõ ràng là quan trọng: nhìn vào chúng, chúng to!</blockquote>
    Hình này được lấy từ bài <a href="https://htmx.org/essays/codin-dirty/" target="_blank">Codin' Dirty</a> của Carson Gross. Bạn sẽ tìm thấy <a href="https://htmx.org/essays/codin-dirty/#real-world-examples" target="_blank">ví dụ thực tế</a> về deep function ở đó.
</details>

P.S. Nếu bạn nghĩ chúng ta đang ủng hộ God object phình to với quá nhiều responsibility, bạn hiểu sai rồi.

## Responsible cho một thing
Quá thường xuyên, chúng ta tạo ra nhiều shallow module, theo một nguyên tắc mơ hồ "một module nên responsible cho một, và chỉ một, thing". Cái "một thing" mơ hồ này là gì? Khởi tạo một object là một thing, đúng không? Vậy [MetricsProviderFactoryFactory](https://minds.md/benji/frameworks) có vẻ ổn. **Tên và interface của các class như vậy có xu hướng tốn não hơn toàn bộ implementation của chúng, đó là abstraction kiểu gì?** Có gì đó sai sai.

Chúng ta thay đổi hệ thống để thỏa mãn user và stakeholder. Chúng ta responsible với họ.

> Một module nên responsible với một, và chỉ một, user hoặc stakeholder.

Đây là bản chất của Single Responsibility Principle. Nói đơn giản, nếu ta gây ra bug ở một chỗ, rồi hai business people khác nhau đến phàn nàn, ta đã vi phạm nguyên tắc. Nó không liên quan gì đến số lượng thing ta làm trong module.

Nhưng ngay cả bây giờ, rule này có thể gây hại nhiều hơn lợi. Nguyên tắc này có thể được hiểu theo nhiều cách khác nhau tùy mỗi người. Approach tốt hơn là nhìn vào lượng cognitive load mà nó tạo ra. Rất tốn não để nhớ rằng thay đổi ở một chỗ có thể trigger chuỗi phản ứng qua các business stream khác nhau. Và chỉ vậy thôi, không cần học fancy term gì cả.

## Quá nhiều shallow microservice
Nguyên tắc shallow-deep module này scale-agnostic, và ta có thể áp dụng nó cho microservices architecture. Quá nhiều shallow microservice không tốt - ngành đang hướng tới "macroservice", tức là service không quá shallow (=deep). Một trong những hiện tượng tệ nhất và khó fix nhất là distributed monolith, thường là kết quả của việc phân tách shallow quá mức này.

Tôi từng tư vấn cho một startup nơi team năm developer tạo ra 17(!) microservice. Họ chậm 10 tháng so với lịch trình và không gần tới public release. Mỗi requirement mới dẫn đến thay đổi trong 4+ microservice. Mất vô cùng nhiều thời gian để reproduce và debug issue trong distributed system như vậy. Cả time to market và cognitive load đều cao không thể chấp nhận. `🤯`

Đây có phải cách đúng để tiếp cận uncertainty của hệ thống mới? Cực kỳ khó để xác định đúng logical boundary ngay từ đầu. Điều quan trọng là đưa ra quyết định càng muộn càng tốt, vì lúc đó bạn có nhiều thông tin nhất. Bằng cách đưa network layer vào ngay từ đầu, ta làm cho design decision khó revert ngay từ lúc bắt đầu. Lý do duy nhất của team là: "Các công ty FAANG đã chứng minh microservices architecture hiệu quả". *Hello, bạn phải thôi mơ lớn đi.*

[Tranh luận Tanenbaum-Torvalds](https://en.wikipedia.org/wiki/Tanenbaum%E2%80%93Torvalds_debate) cho rằng thiết kế monolithic của Linux là lỗi thời và nên dùng microkernel architecture thay thế. Thật vậy, thiết kế microkernel có vẻ vượt trội "từ góc độ lý thuyết và thẩm mỹ". Về mặt thực tế - ba thập kỷ sau, GNU Hurd dựa trên microkernel vẫn đang phát triển, còn monolithic Linux thì ở khắp nơi. Trang này chạy bằng Linux, ấm đun nước thông minh của bạn cũng chạy Linux. Bằng monolithic Linux.

Một monolith được craft tốt với các module thật sự isolated thường linh hoạt hơn nhiều so với một đống microservice. Nó cũng cần ít cognitive effort hơn nhiều để maintain. Chỉ khi nhu cầu deploy riêng biệt trở nên quan trọng, như scale development team, bạn mới nên xem xét thêm network layer giữa các module, các microservice tương lai.

## Ngôn ngữ feature-rich
Chúng ta hào hứng khi các feature mới được release trong ngôn ngữ yêu thích. Chúng ta dành thời gian học các feature này, build code dựa trên chúng.

Nếu có nhiều feature, ta có thể tốn nửa giờ chơi với vài dòng code, để dùng feature này hay feature kia. Và đó hơi lãng phí thời gian. Nhưng tệ hơn, **khi bạn quay lại sau, bạn phải recreate lại thought process đó!**

**Bạn không chỉ phải hiểu chương trình phức tạp này, bạn còn phải hiểu tại sao một programmer quyết định đây là cách tiếp cận vấn đề từ các feature có sẵn.** `🤯`

Những phát biểu này được đưa ra bởi không ai khác ngoài Rob Pike.

> Giảm cognitive load bằng cách giới hạn số lượng choice.

Language feature là OK, miễn là chúng orthogonal với nhau.

<details>
  <summary><b>Suy nghĩ từ một engineer với 20 năm kinh nghiệm C++ ⭐️</b></summary>
  <br>
  Hôm trước tôi nhìn RSS reader và nhận ra có khoảng ba trăm bài chưa đọc dưới tag "C++". Tôi chưa đọc một bài nào về ngôn ngữ này từ mùa hè năm ngoái, và tôi cảm thấy tuyệt!<br><br>
  Tôi đã dùng C++ được 20 năm rồi, gần hai phần ba cuộc đời tôi. Phần lớn kinh nghiệm của tôi là deal với những góc tối nhất của ngôn ngữ (như undefined behaviour đủ loại). Đây không phải kinh nghiệm tái sử dụng được, và hơi đáng sợ khi phải bỏ hết bây giờ.<br><br>
  Kiểu như, bạn có thể tưởng tượng được không, token <code>||</code> có nghĩa khác nhau trong <code>requires ((!P&lt;T&gt; || !Q&lt;T&gt;))</code> và trong <code>requires (!(P&lt;T&gt; || Q&lt;T&gt;))</code>. Cái đầu là constraint disjunction, cái thứ hai là operator logical OR quen thuộc, và chúng hoạt động khác nhau.<br><br>
  Bạn không thể allocate space cho trivial type và chỉ <code>memcpy</code> một set byte vào đó mà không cần thêm effort - điều đó sẽ không bắt đầu lifetime của một object. Đây là tình huống trước C++20. Nó đã được fix trong C++20, nhưng cognitive load của ngôn ngữ chỉ tăng lên.<br><br>
  Cognitive load liên tục tăng, dù mọi thứ được fix. Tôi phải biết cái gì được fix, khi nào nó được fix, và trước đó nó như thế nào. Tôi là một professional mà. Chắc chắn, C++ giỏi về legacy support, điều đó cũng có nghĩa là bạn <b>sẽ gặp</b> legacy đó. Ví dụ, tháng trước một đồng nghiệp hỏi tôi về một behaviour trong C++03. <code>🤯</code><br><br>
  Có 20 cách initialization. Uniform initialization syntax được thêm vào. Bây giờ có 21 cách initialization. Nhân tiện, có ai nhớ rule để chọn constructor từ initializer list không? Một cái gì đó về implicit conversion với ít loss thông tin nhất, <i>nhưng nếu</i> giá trị được biết statically thì... <code>🤯</code><br><br>
  <b>Cognitive load tăng lên này không phải do business task đang làm. Không phải intrinsic complexity của domain. Nó chỉ ở đó do lý do lịch sử</b> (<i>extraneous cognitive load</i>).<br><br>
  Tôi phải nghĩ ra vài rule. Kiểu như, nếu dòng code đó không rõ ràng và tôi phải nhớ standard, tốt hơn là không viết kiểu đó. Standard dài khoảng 1500 trang, nhân tiện.<br><br>
  <b>Tôi hoàn toàn không blame C++.</b> Tôi yêu ngôn ngữ này. Chỉ là tôi mệt rồi.<br><br>
  <p>Cảm ơn <a href="https://0xd34df00d.me" target="_blank">0xd34df00d</a> đã viết.</p>
</details>

## Business logic và HTTP status code
Ở backend ta return:
`401` cho expired JWT token
`403` cho không đủ access
`418` cho banned user

Các engineer ở frontend dùng backend API để implement login functionality. Họ sẽ phải tạm thời tạo cognitive load sau trong đầu:
`401` là cho expired JWT token // `🧠+`, ok chỉ nhớ tạm thời
`403` là cho không đủ access // `🧠++`
`418` là cho banned user // `🧠+++`

Frontend developer sẽ (hy vọng) tạo một loại dictionary `numeric status -> meaning` ở phía họ, để các contributor thế hệ sau không phải recreate mapping này trong đầu.

Rồi QA engineer vào cuộc:
"Hey, tôi nhận được status `403`, đó là expired token hay không đủ access?"
**QA engineer không thể nhảy thẳng vào testing, vì trước tiên họ phải recreate cognitive load mà engineer backend đã tạo.**

Tại sao phải giữ custom mapping này trong working memory? Tốt hơn là abstract business detail ra khỏi HTTP transfer protocol, và return code tự mô tả trực tiếp trong response body:
```json
{
    "code": "jwt_has_expired"
}
```

Cognitive load ở phía frontend: `🧠` (fresh, không có fact nào được giữ trong đầu)
Cognitive load ở phía QA: `🧠`

Rule tương tự áp dụng cho tất cả loại numeric status (trong database hay bất kỳ đâu) - **ưu tiên string tự mô tả.** Chúng ta không còn ở thời đại máy 640K để optimize memory nữa.

> Mọi người dành thời gian tranh luận giữa `401` và `403`, đưa ra quyết định dựa trên mental model riêng của họ. Developer mới vào phải recreate thought process đó. Bạn có thể đã document "why" (ADR) cho code, giúp newcomer hiểu quyết định đã đưa ra. Nhưng cuối cùng nó chẳng có ý nghĩa gì. Ta có thể tách error thành user-related hoặc server-related, nhưng ngoài ra thì mọi thứ hơi mơ hồ.

P.S. Thường rất tốn não để phân biệt giữa "authentication" và "authorization". Ta có thể dùng term đơn giản hơn như ["login" và "permission"](https://ntietz.com/blog/lets-say-instead-of-auth/) để giảm cognitive load.

## Lạm dụng nguyên tắc DRY

Do not repeat yourself - đó là một trong những nguyên tắc đầu tiên bạn được dạy khi là software engineer. Nó được nhúng sâu vào bản thân chúng ta đến nỗi ta không thể chịu được việc có thêm vài dòng code. Mặc dù nhìn chung là một rule tốt và fundamental, khi overuse nó dẫn đến cognitive load mà ta không thể handle.

Ngày nay, mọi người build software dựa trên các component tách biệt về mặt logic. Thường chúng được phân phối giữa nhiều codebase đại diện cho các service riêng. Khi bạn cố gắng loại bỏ mọi repetition, bạn có thể tạo ra tight coupling giữa các component không liên quan. Kết quả là, thay đổi ở một phần có thể có hậu quả ngoài ý muốn ở các khu vực khác có vẻ không liên quan. Nó cũng có thể cản trở khả năng replace hoặc modify từng component mà không ảnh hưởng toàn bộ hệ thống. `🤯`

Thực tế, vấn đề tương tự nảy sinh ngay cả trong một module đơn lẻ. Bạn có thể extract common functionality quá sớm, dựa trên sự giống nhau có thể không thực sự tồn tại về lâu dài. Điều này có thể dẫn đến các abstraction không cần thiết khó modify hoặc extend.

Rob Pike từng nói:

> A little copying is better than a little dependency.

Chúng ta bị cám dỗ để không reinvent bánh xe mạnh đến nỗi sẵn sàng import các library to nặng để dùng một function nhỏ mà ta dễ dàng viết được.

**Tất cả dependency của bạn là code của bạn.** Đi qua 10+ level của stack trace của library đã import và tìm ra chỗ sai (*vì mọi thứ đều sai*) rất đau đớn.

## Tight coupling với framework
Có rất nhiều "magic" trong framework. Bằng cách dựa quá nhiều vào framework, **ta buộc tất cả developer sau này phải học "magic" đó trước.** Có thể mất hàng tháng. Mặc dù framework cho phép ta launch MVP trong vài ngày, về lâu dài chúng có xu hướng thêm complexity và cognitive load không cần thiết.

Tệ hơn, tại một thời điểm nào đó framework có thể trở thành constraint đáng kể khi đối mặt với requirement mới không fit architecture. Từ đây mọi người fork framework và maintain custom version của riêng họ. Tưởng tượng lượng cognitive load mà một newcomer phải build (tức là học custom framework này) để deliver bất kỳ value nào. `🤯`

**Chúng ta hoàn toàn không advocate việc invent mọi thứ from scratch!**

Ta có thể viết code theo cách hơi framework-agnostic. Business logic không nên nằm trong framework; thay vào đó, nó nên dùng các component của framework. Đặt framework ra ngoài core logic của bạn. Dùng framework theo kiểu library. Điều này cho phép contributor mới add value từ ngày đầu tiên, không cần phải đi qua debris của framework-related complexity trước.

> [Why I Hate Frameworks](https://minds.md/benji/frameworks)

## Layered architecture
Có một sự hào hứng về engineering đối với tất cả thứ này.

Bản thân tôi từng là người ủng hộ nhiệt thành Hexagonal/Onion Architecture trong nhiều năm. Tôi dùng nó ở đây và kia và khuyến khích các team khác làm như vậy. Độ phức tạp của project tăng lên, số lượng file tăng gấp đôi. Cảm giác như ta đang viết rất nhiều glue code. Với requirement thay đổi liên tục, ta phải thay đổi qua nhiều layer của abstraction, tất cả trở nên tẻ nhạt. `🤯`

**Abstraction được cho là ẩn complexity, ở đây nó chỉ thêm [indirection](https://fhur.me/posts/2024/thats-not-an-abstraction).** Nhảy từ call này sang call khác để đọc theo và tìm ra chỗ sai và thiếu cái gì là requirement quan trọng để nhanh chóng giải quyết vấn đề. Với việc layer uncoupling của architecture này, nó cần một factor exponential của các trace thêm, thường không liên tục, để đến điểm xảy ra lỗi. Mỗi trace như vậy chiếm chỗ trong limited working memory của ta. `🤯`

<div align="center">
  <img src="/img/layers.png" alt="Layers" width="400">
</div>

Architecture này là thứ có vẻ hợp lý ban đầu, nhưng mỗi lần ta thử áp dụng vào project thì nó gây hại nhiều hơn lợi. Chúng ta dành nhiều năm cho hoạt động tinh thần không cần thiết và viết glue code vô dụng không có business value rõ ràng. Ngược lại, ta làm mọi thứ tệ hơn cho business bằng cách buộc newcomer phải học approach (mental model) của ta trước. Time to market xấu đi. Cuối cùng, ta từ bỏ tất cả để ủng hộ dependency inversion principle cũ kỹ tốt đẹp. **Không có port/adapter term để học, không có layer horizontal abstraction không cần thiết, không có extraneous cognitive load.**

Nếu bạn nghĩ rằng layering như vậy sẽ cho phép bạn nhanh chóng replace database hoặc dependency khác, bạn nhầm rồi. Thay đổi storage gây ra nhiều vấn đề, và tin tôi đi, có một vài abstraction cho data access layer là ít lo lắng nhất của bạn. Tốt nhất, abstraction có thể tiết kiệm khoảng 10% thời gian migration (nếu có), pain thực sự nằm ở data model incompatibility, communication protocol, distributed system challenge, và [implicit interface](https://www.hyrumslaw.com).

> Với đủ số lượng user của một API,
> không quan trọng bạn promise gì trong contract:
> tất cả observable behaviour của hệ thống
> sẽ được ai đó depend vào.

Chúng tôi đã làm storage migration, và mất khoảng 10 tháng. Hệ thống cũ là single-threaded, nên các event exposed là sequential. Tất cả hệ thống của chúng tôi depend vào observed behaviour đó. Behaviour này không phải part của API contract, không được phản ánh trong code. Storage mới distributed không có guarantee đó - các event ra ngoài out-of-order. Chúng tôi chỉ mất vài giờ code storage adapter mới, nhờ abstraction. **Chúng tôi dành 10 tháng tiếp theo để deal với out-of-order event và các challenge khác.** Giờ thật buồn cười khi nói abstraction giúp ta replace component nhanh chóng.

**Vậy, tại sao phải trả giá của cognitive load cao cho layered architecture như vậy, nếu nó không pay off trong tương lai?** Hơn nữa, trong hầu hết trường hợp, tương lai thay thế core component đó không bao giờ xảy ra.

Các architecture này không fundamental, chúng chỉ là hậu quả chủ quan, biased của các nguyên tắc fundamental hơn. Tại sao rely vào những interpretation chủ quan đó? Follow các rule fundamental thay thế: dependency inversion principle, single source of truth, cognitive load và information hiding. Business logic không nên depend vào low-level module như database, UI hay framework. Ta nên có thể viết test cho core logic mà không lo về infrastructure, và chỉ vậy thôi. [Thảo luận](https://github.com/zakirullin/cognitive-load/discussions/24).

Đừng thêm layer abstraction vì architecture. Thêm chúng khi bạn cần extension point được justify bởi lý do thực tế.

**[Layer abstraction không free](https://blog.jooq.org/why-you-should-not-implement-layered-architecture), chúng phải được giữ trong limited working memory của ta.**

## Domain-driven design
Domain-driven design có một vài điểm tốt, mặc dù nó thường bị hiểu sai. Mọi người nói, "Chúng ta viết code trong DDD", hơi lạ, vì DDD nhiều về problem space hơn là solution space.

Ubiquitous language, domain, bounded context, aggregate, event storming đều về problem space. Chúng được dùng để giúp ta học insight về domain và extract boundary. DDD cho phép developer, domain expert và business people giao tiếp hiệu quả bằng một ngôn ngữ đơn nhất, thống nhất. Thay vì focus vào các problem space aspect của DDD này, ta có xu hướng nhấn mạnh folder structure cụ thể, service, repository, và các solution space technique khác.

Rất có thể cách ta interpret DDD là duy nhất và chủ quan. Và nếu ta build code dựa trên sự hiểu biết này, tức là nếu ta tạo ra nhiều extraneous cognitive load - các developer tương lai sẽ khốn khổ. `🤯`

Team Topologies cung cấp framework tốt hơn nhiều, dễ hiểu hơn giúp ta split cognitive load giữa các team. Engineer có xu hướng phát triển mental model hơi giống nhau sau khi học về Team Topologies. DDD, mặt khác, dường như tạo ra 10 mental model khác nhau cho 10 người đọc khác nhau. Thay vì là common ground, nó trở thành battleground cho các cuộc tranh luận không cần thiết.

## Cognitive load trong familiar project

> Vấn đề là **familiarity không giống simplicity.** Chúng *cảm thấy* giống nhau — cùng sự dễ dàng di chuyển qua một không gian mà không cần nhiều mental effort — nhưng vì những lý do rất khác nhau. Mỗi trick "clever" (đọc: "tự chiều chuộng") và non-idiomatic mà bạn dùng tạo ra learning penalty cho mọi người khác. Một khi họ đã học xong, họ sẽ thấy làm việc với code ít khó khăn hơn. Vì vậy khó để nhận ra cách simplify code mà bạn đã quen thuộc. Đây là lý do tôi cố gắng để "the new kid" critique code trước khi họ bị institutionalized quá nhiều!
>
> Rất có thể tác giả trước đã tạo ra mess khổng lồ này từng increment nhỏ, không phải một lần. Vì vậy bạn là người đầu tiên phải cố gắng hiểu tất cả cùng một lúc.
>
> Trong class của tôi, tôi mô tả một SQL stored procedure sprawling mà chúng ta xem một ngày, với hàng trăm dòng conditional trong WHERE clause khổng lồ. Ai đó hỏi làm sao ai có thể để nó tệ đến vậy. Tôi nói với họ: "Khi chỉ có 2 hoặc 3 conditional, thêm một cái nữa không tạo ra khác biệt gì. Đến khi có 20 hoặc 30 conditional, thêm một cái nữa không tạo ra khác biệt gì!"
>
> Không có "simplifying force" tác động lên code base ngoài deliberate choice mà bạn đưa ra. Simplifying cần effort, và mọi người thường quá vội vàng.
>
> *Cảm ơn [Dan North](https://dannorth.net) vì comment của anh ấy*.

Nếu bạn đã internalize mental model của project vào long-term memory, bạn sẽ không trải qua cognitive load cao.

<div align="center">
  <img src="/img/mentalmodelsv15.png" alt="Mental models" width="700">
</div>

Càng nhiều unique mental model để học, càng mất nhiều thời gian để developer mới deliver value. Nếu bạn giữ cognitive load thấp, mọi người có thể contribute vào codebase trong vài giờ đầu khi join công ty. Và điều đó không có nghĩa là ta hy sinh chất lượng, hay cho phép pile of mud xuất hiện.

> Các unique mental model đó là gì? Đó là một set rule, thường là mixture của Clean Architecture/Event Driven Architecture/DDD. Đây là interpretation riêng của tác giả về những thứ khiến anh ta hào hứng nhất. Mental model chủ quan của riêng anh ta. **Extraneous cognitive load mà người khác phải internalize.**

Khi bạn onboard người mới vào project, hãy thử đo lường lượng confusion họ có (pair programming có thể giúp). Nếu họ confused hơn ~40 phút liên tục - bạn có thứ cần cải thiện trong code.

## Ví dụ
> Software system có lẽ là thứ phức tạp nhất và intricate nhất (về số lượng loại part khác nhau) mà nhân loại tạo ra.
>
> *Fred Brooks, The Mythical Man-Month*

- Architecture của chúng ta là standard CRUD app architecture, [một Python monolith trên Postgres](https://danluu.com/simple-architectures/)
- Instagram scale như thế nào tới 14 triệu user với [chỉ 3 engineer](https://read.engineerscodex.com/p/how-instagram-scaled-to-14-million)
- Các công ty nơi chúng ta "woah, những người này [thông minh vãi](https://kenkantzer.com/learnings-from-5-years-of-tech-startup-code-audits/)" phần lớn đã thất bại
- Một function wire up toàn bộ hệ thống. Nếu bạn muốn biết hệ thống hoạt động như thế nào - [đọc nó](https://www.infoq.com/presentations/8-lines-code-refactoring)
- Designing for Understandability: [The Raft Consensus Algorithm](https://www.youtube.com/watch?v=vYp4LYbnnW8)

Các architecture này khá nhàm chán và dễ hiểu. Bất kỳ ai cũng có thể grasp chúng mà không cần nhiều mental effort.

<details>
    <summary><b>Nguyên tắc coding và kinh nghiệm</b></summary>
    <div align="center">
        <img src="img/complexity.png" alt="Super simple code" width="500">
    </div>
    <a href="https://twitter.com/flaviocopes">@flaviocopes</a>
</details>

Involve junior developer vào architecture review, họ sẽ giúp bạn identify các khu vực mentally demanding.

**Maintaining software rất khó**, mọi thứ break và ta cần mọi bit mental effort mà ta có thể tiết kiệm. Càng ít component trong hệ thống, càng ít issue sẽ có. Debug cũng sẽ ít mentally taxing hơn.

> Debug khó gấp đôi so với viết code ngay từ đầu. Do đó, nếu bạn viết code clever nhất có thể, theo định nghĩa, bạn không đủ thông minh để debug nó.
>
> *Brian Kernighan*

Nhìn chung, mindset "Wow, architecture này chắc chắn cảm thấy tốt!" rất misleading. Đó là cảm giác chủ quan "tại một thời điểm", và nó không nói gì về thực tế. Approach tốt hơn nhiều là quan sát hậu quả về lâu dài:
- Có dễ reproduce và debug issue không? Hay bạn phải nhảy qua call stack hoặc distributed component, cố gắng hiểu mọi thứ trong đầu?
- Ta có thể thay đổi nhanh không, hay có nhiều unknown unknown, và mọi người sợ touch mọi thứ?
- Người mới có thể add feature nhanh không? Có unique mental model nào cần học không?

Những câu hỏi này khó track hơn nhiều, và mọi người thường không thích trả lời chúng trực tiếp. Nhìn vào một vài software system phức tạp nhất thế giới, những thứ đã vượt qua thử thách của thời gian - Unix, Kubernetes, Chrome và Redis (xem comment bên dưới). Bạn sẽ không tìm thấy gì fancy ở đó, phần lớn là nhàm chán, và đó là điều tốt.

## Kết luận
Tưởng tượng một chốc rằng cái mà ta suy ra trong chương thứ hai thực ra không đúng. Nếu vậy, thì kết luận mà ta vừa phủ định, cùng với các kết luận trong chương trước mà ta đã chấp nhận là hợp lệ, có thể không chính xác. `🤯`

Bạn cảm thấy nó chứ? Không chỉ bạn phải nhảy khắp bài để lấy nghĩa (shallow module!), mà đoạn văn nói chung khó hiểu. Chúng ta vừa tạo ra unnecessary cognitive load trong đầu bạn. **Đừng làm điều này với đồng nghiệp.**

<div align="center">
  <img src="/img/smartauthorv14thanksmari.png" alt="Smart author" width="600">
</div>

Chúng ta nên giảm bất kỳ cognitive load nào ngoài cái vốn có trong công việc chúng ta làm.

---
[LinkedIn](https://www.linkedin.com/in/zakirullin/), [X](https://twitter.com/zakirullin), [GitHub](https://github.com/zakirullin), artemzr(аt)g-yоu-knоw-com

## Comment

**Rob Pike** *(Unix, Golang)*  
Bài viết hay.

**[Andrej Karpathy](https://x.com/karpathy/status/1872038630405054853)** *(ChatGPT, Tesla)*  
Bài post hay về software engineering. Có lẽ là quan điểm đúng nhất, được thực hành ít nhất.

**[Elon Musk](https://x.com/elonmusk/status/1872346903792566655)** *(Rocket)*  
Đúng.

**[Addy Osmani](https://www.linkedin.com/feed/update/urn:li:activity:7277757844970520576/)** *(Chrome, software system phức tạp nhất thế giới)*  
Tôi đã thấy vô số project nơi developer thông minh tạo ra architecture ấn tượng bằng design pattern mới nhất và microservice. Nhưng khi team member mới cố gắng thay đổi, họ mất hàng tuần chỉ để hiểu mọi thứ fit với nhau như thế nào. Cognitive load cao đến nỗi productivity giảm mạnh và bug nhân lên.

Mỉa mai? Nhiều pattern gây complexity này được implement với danh nghĩa "clean code."

Điều thực sự quan trọng là giảm unnecessary cognitive burden. Đôi khi điều này có nghĩa là ít module sâu hơn thay vì nhiều shallow module. Đôi khi có nghĩa là giữ logic liên quan với nhau thay vì tách thành các function nhỏ.

Và đôi khi có nghĩa là chọn solution nhàm chán, straightforward hơn là clever. Code tốt nhất không phải elegant hoặc sophisticated nhất - đó là code mà developer tương lai (bao gồm cả bạn) có thể hiểu nhanh chóng.

Bài viết của bạn thực sự cộng hưởng với các challenge chúng tôi đối mặt trong browser development. Bạn hoàn toàn đúng về browser hiện đại là một trong những software system phức tạp nhất. Quản lý complexity đó trong Chromium là challenge liên tục align hoàn hảo với nhiều điểm bạn đưa ra về cognitive load.

Một cách chúng tôi cố gắng handle điều này trong Chromium là thông qua component isolation cẩn thận và well-defined interface giữa các subsystem (như rendering, networking, JavaScript execution, v.v.). Tương tự ví dụ deep module của bạn với Unix I/O - chúng tôi aim cho powerful functionality đằng sau interface tương đối đơn giản. Ví dụ, rendering pipeline của chúng tôi handle incredible complexity (layout, compositing, GPU acceleration) nhưng developer có thể tương tác với nó thông qua clear abstraction layer.

Các điểm của bạn về tránh unnecessary abstraction cũng rất trúng. Trong browser development, chúng tôi liên tục cân bằng giữa làm codebase approachable cho contributor mới trong khi handle inherent complexity của web standard và compatibility.

Đôi khi solution đơn giản nhất là tốt nhất, ngay cả trong complex system.

**[antirez](https://x.com/antirez)** *(Redis)*  
Hoàn toàn đồng ý :) Ngoài ra, cái tôi tin là thiếu trong "A Philosophy of Software Design" đã đề cập là khái niệm "design sacrifice". Tức là, đôi khi bạn sacrifice thứ gì đó và nhận lại simplicity, hoặc performance, hoặc cả hai. Tôi áp dụng ý tưởng này liên tục, nhưng thường không được hiểu.

Một ví dụ tốt là việc tôi luôn từ chối có hash item expire. Đây là design sacrifice vì nếu bạn có certain attribute chỉ trong top-level item (các key chính chúng), thiết kế đơn giản hơn, value sẽ chỉ là object. Khi Redis có hash expire, đó là nice feature nhưng yêu cầu (thật vậy) nhiều thay đổi cho nhiều part, tăng complexity.

Một ví dụ khác là cái tôi đang làm ngay bây giờ, Vector Set, Redis data type mới. Tôi quyết định rằng Redis sẽ không là source of truth về vector, mà nó chỉ có thể lấy approximate version của chúng, nên tôi có thể làm on-insert normalization, quantization mà không cố gắng retain large float vector trên disk, v.v. Nhiều vector DB không sacrifice việc nhớ cái user đưa vào (full precision vector).

Đây chỉ là hai ví dụ random, nhưng tôi áp dụng ý tưởng này ở mọi nơi. Bây giờ vấn đề là: dĩ nhiên người ta phải sacrifice đúng thứ. Thường có 5% feature chiếm very large amount của complexity: đó là thứ tốt để kill :D

**[Một developer từ internet](https://working-for-the-future.medium.com/about)**  
Bạn sẽ không hire tôi... Tôi bán mình dựa trên track record của các enterprise project đã release.

Tôi làm việc với một người có thể nói về design pattern. Tôi không bao giờ có thể nói kiểu đó, mặc dù tôi là một trong số ít có thể hiểu anh ta rõ ràng. Các manager yêu thích anh ta và anh ta có thể dominate bất kỳ development conversation nào. Những người làm việc xung quanh anh ta nói anh ta để lại trail of destruction phía sau. Người ta nói với tôi rằng tôi là người đầu tiên có thể hiểu project của anh ta. Maintainability quan trọng. Tôi quan tâm nhất về TCO (*Total Cost of Ownership*). Với một vài firm, đó là thứ quan trọng.

Tôi đăng nhập Github sau khi không ở đó một thời gian và vì lý do nào đó nó đưa tôi đến một bài trong repository của ai đó có vẻ random. Tôi nghĩ "cái gì đây" và gặp chút rắc rối để đến home page, nên tôi đọc nó. Tôi không thực sự register nó vào lúc đó, nhưng nó tuyệt vời. Mọi developer nên đọc nó. Nó phần lớn nói rằng hầu như mọi thứ chúng ta được nói về programming best practice dẫn đến "cognitive load" quá mức, có nghĩa là đầu óc của chúng ta bị đá bởi intellectual demand. Tôi đã biết điều này một thời gian, đặc biệt với các demand của cloud, security và DevOps.

Tôi cũng thích nó vì nó mô tả practice tôi làm trong hàng thập kỷ, nhưng không bao giờ thừa nhận vì chúng không popular... Tôi viết stuff thực sự phức tạp và cần mọi help tôi có thể nhận được.

Cân nhắc, nếu tôi đúng, nó pop up vì các Github folk, những người rất thông minh, nghĩ rằng developer nên thấy nó. Tôi đồng ý.

[Comment trên Hacker News](https://news.ycombinator.com/item?id=45074248) ([2](https://news.ycombinator.com/item?id=42489645))
