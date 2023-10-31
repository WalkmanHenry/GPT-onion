# 2⃣ 第二天 技术选型与TDD

## 第二天 技术选型

我们拿到了完整的PRD以后，现在要开始分析项目并且决定需要采用的技术。

### 2.1 苏格拉底式提问

核心的逻辑还是为了完成产品的功能需求。

解决问题的方法，不是第一时间想答案，而是继续问问题。 而最好的提问方式就是苏格拉底式提问。

> 苏格拉底式提问(Socratic Questioning)是一种启发性的提问方式,通常用于导引对方深入思考和发现答案。

把自己代入提问者和回答者两种身份，**可以做到:**

1. **使用一系列开放式问题引导我们思考** 苏格拉底式提问重在提出问题,而不是给出答案。提问者通过构建问题链,引导我们一步步深入思考问题的本质。
2. **激发批判性思维** 这种提问方式会激发对方的思维,鼓励我们提出自己的看法,并对答案进行质疑和批判性思考。
3. **帮助我们发现答案** 提问者并不给出答案,而是通过提问让我们自己得出结论,从而深入理解并内化知识。
4. **推动对话深入** 苏格拉底式提问可以把对话推进到更深的层次,挖掘出对方的假设,展开知识的层层推理。
5. **增强学习能力** 这种提问可以培养对方的独立思考能力和学习能力,使我们在以后可以主动发问和解决问题。

从一开始分析产品，我们就确定了**产品的形式是网站**。 那么从这里开始苏格拉底式提问：

* **为什么不是手机应用**：
  * 时间不够，网站相比手机应用在开发周期上更短，适用性更广。
    * **时间够就是手机应用？** 好像没有理由否决，谁说不能是手机应用？
  * 电脑屏幕更大，有更好的聊天体验。
    * **手机不能通过优化体验来实现相同功能吗？** 理论上可以，所以可以考虑手机应用。
  * 使用电脑的时候操作效率更高，且是在工作。
    * **用手机不能工作吗？** 可以，但是效率目前会有差距，而且短时间内好像很难弥补。
    * **那表示没有移动端需求了吗？** 显然不是，而且可能存在不同的场景和用户习惯，但是目前来做这方面的功能，投入产出比不高。

你看，通过不断的提问，我们能够想清楚很多细节。

移动端和PC端，两者的底层逻辑相同，且大量可以复用的代码，所以可以在选择技术的时候照顾后续的手机应用做系统架构。

**从性能和技术实施的方向考虑问题**：

1. **可能的挑战**：
   * 某个提示词火热的时候带来的峰值可能会产生OpenAI的接口调用拥堵。
   * 由于是UGC内容，因此Prompt的增长肯能会非常快，如何提前考虑分表分库。
   * 聊天内容是大段的文字，是否有搜索需求，如何能够减少IO次数，如何能够减少对数据库效率的影响。
2. **可能存在的技术问题**：
   * 相对于新闻类网站，有更大的数据库压力。
3. **用户体验**:
   * 选择能够提供高质量用户体验的技术，包括加载速度、交互性和可用性。
   * 考虑技术选型对移动端和不同浏览器的支持程度。
4. **性能和可扩展性**:
   * 评估不同技术的性能，包括响应时间、并发处理能力和数据处理能力。
   * 考虑项目可能的增长和扩展，确保技术有良好的可扩展性和可维护性。
5. **安全性**:
   * 评估技术的安全性，确保能够满足项目的安全需求和合规要求。
   * 考虑技术对于常见安全威胁的防护能力，例如SQL注入、跨站脚本等。

**从成本的角度考虑问题**：

1. **开发效率和成本**:
   * 评估技术选型对开发周期的影响，选择能够提高开发效率的技术。
   * 考虑技术的成本效益，包括开发成本、维护成本和运营成本。
2. **技术生态和社区支持**:
   * 选择有活跃社区和丰富资源的技术，以便在遇到问题时能够快速找到解决方案。
   * 考虑技术的更新和维护情况，确保技术的持续发展和支持。
3. **团队的技能和经验**:
   * 考虑团队的技能和经验，选择团队熟悉或能够快速上手的技术。
   * 考虑是否需要为团队提供额外的培训或资源，以支持技术的采用和应用。
4. **未来的技术发展趋势**:
   * 了解行业的技术发展趋势，避免选择可能会过时或被淘汰的技术。
   * 考虑技术对新技术和标准的支持程度，以保持项目的技术领先性。
5. **与外部系统的集成**:
   * 考虑技术选型对与外部系统和服务的集成的支持，包括API集成、数据交换等。
6. **可测试性和可维护性**:
   * 选择能够支持自动测试、持续集成和持续部署的技术，以提高项目的质量和可维护性。
   * 考虑技术的文档、调试工具和监控工具，以支持项目的开发和运维。

### 2.2 技术选型

#### 2.2.1 前端

前端语言是Javascript没跑了，但是选择使用什么框架？需要额外注意什么问题？

jQuery是优秀的库，但是不属于框架，它没有提供像Vue、React或Angular那样的结构化开发模式。而且随着现代浏览器的发展，很多 jQuery 提供的功能现在可以通过原生JavaScript实现。所以我们优先选择完整框架。

当下热门的框架优先考虑，如果一个项目后期需要新增人手，成本也是重要的考虑方向，所以我们对比一下Vue, React和Angular。

**前端框架比较**

以下是几个热门的前端框架，每个框架都有其特定的优势和劣势：

| 框架/特点       | 优点                                                                                     | 缺点                                       |
| ----------- | -------------------------------------------------------------------------------------- | ---------------------------------------- |
| **Vue**     | <p>- 易于上手: 简单明了的学习曲线<br>- 灵活性: 适应多种项目需求<br>- 社区: 活跃的社区和丰富的插件生态<br>- 代码组织: 组件化的代码组织</p> | - 社区规模: 相比React和Angular可能略微小一些           |
| **React**   | <p>- 巨大的社区: 庞大和活跃的社区<br>- 高性能: 虚拟DOM技术<br>- 可复用组件: 组件化的结构<br>- JSX: 便于创建用户界面</p>       | - 学习曲线: 对新手稍微陡峭                          |
| **Angular** | <p>- 全面的框架: 提供全面解决方案<br>- 类型安全: TypeScript提供类型安全<br>- 优秀的CLI: 快速生成和管理项目代码</p>          | <p>- 学习曲线: 较陡峭<br>- 框架较重: 不适合一些简单的项目</p> |

**代入项目分析**

对于GPT-Onion，主要是一个以社区为中心的AI提示词库平台，有以下几点考量：

* **组件复用和管理**：所有框架都提供了组件化的代码组织，可以帮助我们创建和管理可复用的UI组件。
* **社区和生态系统**：React和Vue有着较为活跃的社区和丰富的插件生态，可以帮助我们找到需要的库和工具。
* **学习曲线**：由于受限于时间，对某个框架更为熟悉，可以倾向于选择那个框架。Vue和React相对于Angular来说学习曲线更为友好。
* **性能**：React和Vue通常能提供较高的性能，特别是在处理大量动态页面更新时。
* **项目复杂度**：如果项目计划非常庞大且复杂，可能会倾向于选择Angular，因为它提供了一个全面的解决方案。而Vue和React在简单和中等复杂度的项目中可能更为适用。

> 对于今后可能出现手机应用，而最简单的处理方式是通过ionic之类的框架实现。这一点上面三个框架都能快速融合。

综合考虑，Vue会是一个相对简单且灵活的解决方案。

#### 2.2.3 后端技术选型

既然是作为Web服务，那么第一考虑的肯定是PHP了，从开发效率的角度讲，远高于Golang和Java；从Web开发友好上来说，也是要好过Golang一大截。

但是，开发效率显然不是唯一的考量要素。

在考虑后端技术选型时，需要考虑以下几个方面：

1. **性能**:
   * 不同的后端技术在处理请求和执行逻辑时的性能会有很大的差异。
   * Golang这样的编译型语言显然会比Node.js、PHP和Ruby快很多。
   * 而Python在Web的应用场景下性能是落后于上述语言的。
2. **可伸缩性**:
   * 选择的技术需要能够随着用户基数的增加而垂直或水平扩展。
   * 垂直扩展方面，Java可以通过增加JVM的堆大小来提高单个实例的处理能力，PHP可以使用Opcode缓存，Go可以考虑如何利用好goroutines。
   * 水平扩展方面，利用Kubernetes、负载均衡设备三者都能轻松解决
3. **安全性**:
   * 保护应用程序和数据的安全是至关重要的。不同的技术和框架可能会有不同的安全特性和最佳实践。
4. **社区支持和生态系统**:
   * 一个活跃的社区和丰富的库/框架生态系统可以大大加速开发进程，并提供解决特定问题的资源。
   * Python 有一个巨大而活跃的社区。这意味着遇到问题时，通常可以在 Stack Overflow 或其他社区论坛上找到答案。
   * 由于 Java 已经存在了很长时间，并且被广泛用于企业级应用，其社区资源丰富，拥有大量的文档、库和框架。
   * Go 是这四种语言中相对较新的，社区活跃度是存在的，但是沉淀相对较少。
   * PHP 社区很大，有很多资源和库，但与 Python 或 Java 相比，它可能不那么活跃。
5. **维护性**:
   * 代码是否易于维护和更新是一个重要的考虑因素，这也包括了文档的完善程度和编码规范的一致性。
   * 同时还包括该语言是否有类似Python的PEP 8，PHP的PEAR这样的官方推荐的编码规范，当研发团队的背景不同，甚至地域各异的情况下，一致的编码规范会减少很多不必要的麻烦。
6. **学习曲线**:
   * 如果团队对选定的技术不熟悉，学习曲线可能会影响项目进度。
7. **成本**:
   * 包括开发、部署和运营成本。
   * Java由于其运行时的资源占用，整体规模很大的时候，运维成本是明显高于Golang和PHP的。
8. **测试和调试工具**:
   * 良好的测试和调试工具可以大大提高开发效率和代码质量。
9. **集成**:
   * 如果项目需要集成第三方服务或系统，需要考虑后端技术的集成能力和灵活性。
   * 项目需要用到Open AI的接口，可以直接使用CURL，这几种常用语言也有sdk，所以相差无几。
10. **长期支持和版本稳定性**:
    * 选择一个有长期支持和版本稳定的技术，可以减少未来可能出现的技术债务。
    * 显然这几种语言都是可选项。
11. **开发人员的经验和喜好**:
    * 团队的技术背景和喜好也是一个需要考虑的因素，因为它会影响开发的速度和质量。

**思考**

所以结合我们项目的特性，

* 考虑后期负载压力，Golang是最优选择。
* 考虑开发效率，Python和PHP是最优选择。
* 考虑成本，Golang和PHP最优。
* 测试和调试差距不大。
* 项目集成方面，差距不大。
* 安全性方面差距不大。

因为成本、开发效率的考量， Java先被我们排除在外，

前端如果通过单页面的形式来减少渲染和传输过程中的数据量， 那么后端只需要以接口的形式响应就好。 Golang和PHP成为最优解。

PHP在session等web服务各方面都优于Golang， 开发效率方面，7天的时间，似乎更适合项目。 Golang是否还能一拼？

#### 2.3 转语言和多语言并行

> 在很多大型项目里，都出现过转语言或多语言的现象。 本质是利用不同语言的特性，解决特定问题。

在我们的项目中，是否有必要用到多语言？ 如果从一开始选定一个最终语言，能节约很多后期转语言的时间，也能减少配置多位不同语言程序员的成本，同时还能在团队规模较小的情况下，降低风险。 那么有哪些转语言或者多语言的成功案例？

* Alibaba：阿里巴巴内部以Java为主，但是到了服务器运维方面，Python能在短时间解决大量问题，包括代码服务调度，在CI/CD方面有很好的表现。而且运维人员就能轻松操作，不需要关注业务的程序员的参与。
* Instagram: 最初，Instagram 的后端是用 Python 的 Django 框架编写的。随着用户量的增长，为了提高性能和效率，Instagram 的团队对其代码进行了大量的优化，并继续使用 Python，但他们也引入了其他技术和语言，如 Golang。
* Twitter: 最初，Twitter 的后端是用 Ruby on Rails 构建的。随着用户数量的增长，为了提高性能和可伸缩性，Twitter 逐渐将其核心组件迁移到了 Scala 和 JVM（Java 虚拟机）上。
* Dropbox: 虽然 Dropbox 的主要代码是用 Python 写的，但为了性能和效率，他们的团队在某些关键部分引入了 Go 和 Rust。
* WhatsApp: 在其早期，WhatsApp 的服务器是用 Erlang 编写的，这有助于其高并发的需求。然而，随着功能和需求的增长，他们也开始使用其他语言，如 C++。
* Slack: Slack 的原始代码是用 PHP 写的，但为了提高性能，他们逐渐将关键部分的代码迁移到了 Java 和 Hack（由 Facebook 开发的 PHP 方言）。
* Shopify: Shopify 的核心代码是用 Ruby on Rails 编写的。但随着其增长和性能需求的变化，他们开始在某些部分使用 Go 语言。

在看到我们的项目，GPT-Onion在后期访问请求增多的情况下，**流式回复**会带来一些问题：

1. 连接持续时间：使用流式回复时，连接会被打开并保持活跃更长的时间，尤其是当数据流动地比较慢或数据量很大时。这意味着在给定的时间内，更多的连接可能会保持打开状态，从而占用服务器的并发连接资源。
2. 并发限制：大多数服务器和操作系统都有并发连接数的上限。超出这个限制可能会导致新的连接请求被拒绝或系统资源被耗尽。
3. 资源使用：除了并发连接本身，持续的连接可能会消耗其他系统资源，如内存、文件描述符或其他关联的网络资源。
4. 其他影响：流式回复可能会影响到其他系统部分，如负载均衡器或反向代理，因为这些设备/软件可能需要跟踪和管理更多的活动连接。当然我们也可以根据URI规则跳过一些。

尽管存在上述的开销和限制，流式回复也有其优势。它可以提供更好的用户体验，尤其是在需要实时更新或大量数据传输的情况下。此外，它可能会减少服务器上的内存使用，因为不需要在内存中缓存整个响应。

抛开Golang不谈，PHP/Python/Java在流式回复的场景下，服务器资源的开销都不小。 如果要展开说的话：

1. **内存回收机制**：
   * **PHP**：PHP 使用引用计数以及周期性垃圾回收机制来管理内存。每个请求结束后，PHP 会尝试释放与该请求相关的所有资源。长时间的流式回复可能会增加内存使用，但这主要取决于处理请求的具体代码。
   * **Python**：Python 使用引用计数和周期性垃圾回收来管理内存。流式回复在 Python 中可能会增加内存使用，但这同样取决于具体的代码实现和数据处理。
   * **Java**：Java 使用基于代的垃圾回收机制。长时间运行的流式回复可能会使老年代堆积更多对象，从而增加垃圾回收的次数和开销。
2. **单个请求占用时间**：
   * **PHP**：传统上，PHP 是用于处理短生命周期的请求的，每个请求启动和终止都有一定的开销。长时间运行的请求可能会更有效地使用资源，因为初始化开销在整个请求生命周期中被摊销。
   * **Python**：Python 通常可以有效地处理长时间运行的请求，尤其是使用像 Tornado 这样的异步框架。
   * **Java**：Java 很适合长时间运行的请求，尤其是在使用了 Servlets、Netty 等技术的情况下。
3. **Lifetime 机制**：
   * **PHP**：PHP 的生命周期通常与请求绑定。这意味着长时间的流式回复可能会受到 PHP 的 `max_execution_time` 配置的限制。
   * **Python**：Python 进程的生命周期通常独立于单个请求，所以它不受到与 PHP 类似的限制。
   * **Java**：Java 应用（例如基于 Tomcat 的应用）的生命周期也独立于单个请求，因此它可以很好地处理长时间的流式回复。

总的来说，这三种语言在处理流式回复时都有其优点和局限性。Java 由于其垃圾回收机制、长时间运行的进程和多线程能力，通常被认为是处理流式和长时间连接的理想选择。Python，尤其是当使用异步框架时，也可以非常有效。而 PHP，虽然不是传统上用于流式回复的选择，但在适当的配置和环境下也能处理得很好。

那么处理流式请求时，Golang跟他们相比，又有哪些明显优势呢？

1. **轻量级并发**：
   * **Goroutines**：Go 使用 goroutines 作为其主要的并发机制。goroutines 是非常轻量级的，这意味着你可以同时启动数十万或数百万个 goroutines 而不会耗尽系统资源。这与 Java 的线程或 Python 的线程/协程相比具有明显的优势。
2. **原生支持并发**：
   * Go 从设计之初就考虑到了并发。这与 Python（后来通过 asyncio 或其他库增加并发支持）和 PHP（通常依赖外部扩展进行并发处理）形成对比。
3. **Channels**：
   * Go 的 channels 提供了一种内置的、类型安全的方式来进行 goroutines 之间的通信，这使得构建复杂的并发模式变得更加简单和直观。
4. **性能和资源使用**：
   * Go 是编译型语言，编译为机器代码，通常比解释型语言（如 Python 和 PHP）更快。同时，Go 的静态类型系统和直接的内存管理通常会导致更有效的资源使用。
5. **标准库**：
   * Go 的标准库为网络编程、HTTP 服务器和客户端以及其他与流式请求相关的任务提供了广泛的支持。这意味着我们可以使用原生工具而不是依赖外部库。
6. **简化的错误处理**：
   * Go 有其特有的错误处理模式，虽然某些开发者可能觉得它有些啰嗦，但它鼓励明确和直接地处理错误，这在流式请求中尤为重要，因为这种请求可能会遇到各种网络或数据中断的问题。
7. **跨平台一致性**：
   * Go 应用可以容易地在多个平台上编译和运行，不需要任何外部依赖。这提供了一种跨平台的一致性，与需要运行时或虚拟机的 Java 或特定解释器的 PHP/Python 形成对比。

显而易见，Golang 由于其并发原语、性能特性和强大的标准库，对于处理流式请求和其他高并发任务非常适合。这并不是说其他语言不能处理这些任务，但 Golang 提供了一种更简洁、高效的方式来实现这些功能。

似乎，Golang是最终解法。 那么，7天的时间，Golang真的能够开发出这样的系统吗？