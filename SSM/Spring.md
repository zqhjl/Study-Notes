- {: id="20210314215617-mob11h6"}### Spring框架两大核心机制
  {: id="20210314215617-uxecn4c" updated="20210314215627"}

  - {: id="20210319181138-3lgxo0m"}Spring是一个企业级开发框架，是软件设计层面的框架，优势在于可以将应用程序进行分层，开发者可以自主选择组件
    {: id="20210314215629-2bur0ze" updated="20210319182401"}

    - {: id="20210314215629-dvm9302"}MVC：Struts2、 Spring MVC
      {: id="20210319181138-eqc41zf" updated="20210319181442"}
    - {: id="20210314220347-1dkq2u7"}ORMapping：Hibernate. MyBatis, Spring Data
      {: id="20210314220347-cs9y9iw" updated="20210314220347"}
    {: id="20210314220350-jnatj4i"}
  - {: id="20210314220349-di4kj0z"}Spring核心技术
    {: id="20210314220349-2hcbprd"}

    - {: id="20210314220406-7wqcxx8"}控制反转（IoC：Inversion of Control）/依赖注入（D|:Dependency Injection）
      {: id="20210314220406-o49nlay" updated="20210319182356"}
    - {: id="20210314220440-johlpfq"}面向切面编程（AOP：Aspect Oriented Programming）
      {: id="20210314220440-zpzluwu" updated="20210314220446"}
    {: id="20210314220505-8ym8uts"}
  - {: id="20210314220504-65qfnxu"}控制反转
    {: id="20210314220504-klp9nfc" updated="20210314220514"}

    - {: id="20210314220514-yydg0pm"}什么是控制反转
      {: id="20210314220514-ztdv2ib"}

      - {: id="20210314220535-g3xexdu"}在传统的程序开发中，需要调用对象时，通常由调用者来创建被调用者的实例，即对象是由调用者主动new出来的。但在 Spring框架中创建对象的工作不再由调用者来完成，而是交给loc容器来创建，再推送给调用者，整个流程完成反转，所以是控制反转。
        {: id="20210314220535-zf3642c" updated="20210319181533"}
      {: id="20210314222424-4r1e21c"}
    - {: id="20210314222423-yhlxa63"}loC底层原理
      {: id="20210314222423-60zyh0r"}

      - {: id="20210314222437-m0g4n35"}读取配置文件，解析XML
        {: id="20210314222437-1vcn1vp" updated="20210314222446"}
      - {: id="20210314222441-zm2m72h"}通过反射机制实例化配置文件中所配置所有的bean
        {: id="20210314222441-nad52ak" updated="20210314222441"}
      {: id="20210314222656-vypwnti"}
    - {: id="20210314222656-ufxeyre"}scope作用域
      {: id="20210314222656-bxyk4v6"}

      - {: id="20210314222700-i7cq30l"}Spring管理的bean是根据sope来生成的，表示bean的作用域，共4种
        {: id="20210314222700-f1pjlzv" updated="20210314222708"}

        - {: id="20210314222708-rsuffaf"}singleton（缺省）：单例，表示通过 Spring容器获取的bean是唯一的
          {: id="20210314222708-gk6ztci" updated="20210314223003"}
        - {: id="20210314222716-84vu7un"}prototype：原型，表示通过 Spring容器获取的bean是不同的
          {: id="20210314222716-5v2qdiz" updated="20210314222719"}
        - {: id="20210314222725-got71yv"}request：请求，表示在一次HTTP请求内有效
          {: id="20210314222725-12x3zx1" updated="20210314222747"}
        - {: id="20210314222728-hdara14"}session：会话，表示在一个用户会话内有效
          {: id="20210314222728-33k15nm" updated="20210314222736"}
        {: id="20210314222803-b29d1nx"}
      - {: id="20210314222740-r8o3txu"}request和 session只适用于Web项目，大多数情况下，使用单例和原型较多。
        {: id="20210314222740-4jhue1b" updated="20210314222740"}
      - {: id="20210314223231-lfqv7li"}prototype模式当业务代码获取loC容器中的bean时， Spring才去调用无参构造创建对应的bean。
        {: id="20210314223231-ejkvtn8"}
      - {: id="20210314223235-457620u"}singleton模式无论业务代码是否获取loC容器中的bean, Spring在加载 spring. XML时就会创建bean
        {: id="20210314223235-nvk5786" updated="20210314223406"}
      {: id="20210314223407-hhdxlzc"}
    - {: id="20210314223406-0vdjgau"}Spring的继承
      {: id="20210314223406-q3qdadc"}

      - {: id="20210314223413-7fjhsph"}与Java的继承不同，Java是类层面的继承，子类可以继承父类的内部结构信息； Spring是对象层面的继承，子对象可以继承父对象的属性值
        {: id="20210314223413-wdwwo9p" updated="20210314223413"}
      - {: id="20210314223811-igzuyxi"}Spring的继承关注点在于具体的对象，而不在于类，即不同的两个类的实例化对象可以完成继承，前提是子对象必须包含父对象的所有属性，同时可以在此基础上添加其他的属性
        {: id="20210314223811-7jq5irn"}
      {: id="20210314223917-uev61b0"}
    - {: id="20210314223917-mndjz0n"}Spring的依赖
      {: id="20210314223917-vh2wfwm"}

      - {: id="20210314223929-bhh8imk"}与继承类似，依赖也是描述bean和bean之间的一种关系，配置依赖之后，被依赖的bean一定先创建，再创建依赖的bean，A依赖于B，先创建B，再创建A。
        {: id="20210314223929-sh0799w" updated="20210314223939"}
      {: id="20210314224201-oujd9mk"}
    - {: id="20210314224200-wcmnd3y"}Spring的p命名空间
      {: id="20210314224200-e66n0ck" updated="20210314224234"}

      - {: id="20210314224234-zweehyd"}p命名空间是对loC/DI的简化操作，使用p命名空间可以更加方便的完成bean的配置以及bean之间的依赖注入。
        {: id="20210314224234-uornwqb" updated="20210314224246"}
      {: id="20210314224550-29l8pkz"}
    {: id="20210314224550-76db7qx"}
  - {: id="20210314224549-q7uexii"}AOP
    {: id="20210314224549-ia3i9yi" updated="20210314224553"}

    - {: id="20210314224555-v4hizlo"}AOP:Aspect Oriented Programming面向切面编程。
      {: id="20210314224555-72lcie9"}

      - {: id="20210314224731-swxrofj"}AOP的优点
        {: id="20210314224731-1xqmtpw" updated="20210314224731"}

        - {: id="20210314224736-r3p8z8y"}降低模块之间的耦合度。
          {: id="20210314224736-u2f9bzq" updated="20210314224736"}
        - {: id="20210314224739-mzx7m36"}使系统更容易扩展。
          {: id="20210314224739-gf5alk1" updated="20210314224739"}
        - {: id="20210314224740-i4vqwd4"}更好的代码复用。
          {: id="20210314224740-m0koebf" updated="20210314224742"}
        - {: id="20210314224743-97j9rvr"}非业务代码更加集中，不分散，便于统一管理
          {: id="20210314224743-3o281mx" updated="20210314224743"}
        - {: id="20210314224745-kiwabs9"}业务代码更加简洁存粹，不参杂其他代码的影响。
          {: id="20210314224745-dbjpwqk" updated="20210314224745"}
        {: id="20210314224749-7ji80pj"}
      - {: id="20210314224748-s42ed6l"}AOP是对面向对象编程的一个补充，在运行时，动态地将代码切入到类的指定方法、指定位置上的编程思想就是面向切面编程。将不同方法的同一个位置抽象成一个切面对象，对该切面对象进行编程就是AOP
        {: id="20210314224748-vcvcqt1" updated="20210319180934"}
      {: id="20210314230157-ts9eohw"}
    {: id="20210314230158-nsvqnwa"}
  {: id="20210314230230-3hm9w2q"}
- {: id="20210314230156-fp2lhm5"}### Spring MVC
  {: id="20210314230156-a483hqf" updated="20210314230238"}

  - {: id="20210314230239-plvjvvn"}Spring mvc概述
    {: id="20210314230239-1jdys7z"}

    - {: id="20210314230257-4wyi1n3"}SpringMVC是目前主流的实现MvC设计模式的框架，是 Spring框架的一个分支产品，以 Spring IoC容器为基础，并利用容器的特性来简化它的配置SpringMVC相当于 Spring的一个子模块，可以很好的和 Spring结合起来进行开发，是 Java Web开发者必须要掌握的框架。
      {: id="20210314230257-nbad25v" updated="20210314230317"}
    {: id="20210314230524-qe5vhau"}
  - {: id="20210314230523-xhol6l4"}什么是MVC设计模式？
    {: id="20210314230523-xatw6ra" updated="20210314230529"}

    - {: id="20210314230531-ah1ak36"}将应用程序分为 Controller、 Model、View三层， Controller接收客户端请求，调用Model生成业务数据，传递给View
      {: id="20210314230531-klxqa02" updated="20210314230554"}
    - {: id="20210314230556-pzt1gyn"}Spring MvC就是对这套流程的封装，屏蔽了很多底层代码，开放岀接口，让开发者可以更加轻松、便捷地完成基于MVC模式的Web开发。
      {: id="20210314230556-6ubplxk" updated="20210314230608"}
    {: id="20210314232029-3xru8vk"}
  - {: id="20210314232027-5f49408"}Spring Mvc的核心组件
    {: id="20210314232027-j98wtje" updated="20210314232127"}

    - {: id="20210314232128-xpjiz9q"}DispatcherServlet：前置控制器，是整个流程控制的核心，控制其他组件的执行，进行统一调度，降低组件之间的耦合性，相当于总指挥
      {: id="20210314232128-ma0dkf7" updated="20210314232132"}
    - {: id="20210314232158-fx6mons"}Handler：处理器，完成具体的业务逻辑，相当于 Servlet或 Action
      {: id="20210314232158-4ukivs3" updated="20210314232158"}
    - {: id="20210314232133-ektzxic"}HandlerMapping:DispatcherServlet接收到请求之后，通过 HandlerMapping将不同的请求映射到不同的Handle
      {: id="20210314232133-ph1pq6a" updated="20210314232137"}
    - {: id="20210314232138-zcg8rl3"}HandlerInterceptor：处理器拦截器，是一个接口，如果需要完成一些拦截处理，可以实现该接口。
      {: id="20210314232138-e2ouwr3" updated="20210314232141"}
    - {: id="20210314232142-22589s1"}Handler Execution Chain：处理器执行链，包括两部分内容：Handler和 HandlerInterceptor（系统会有一个默认的 HandlerInterceptor，如果需要额外设置拦截，可以添加拦截器）
      {: id="20210314232142-q7rr96o" updated="20210314232145"}
    - {: id="20210314232146-ir941h8"}HandlerAdapter：处理器适配器， Handler执行业务方法之前，需要进行一系列的操作，包括表单数据的验证、数据类型的转换、将表单数据封装到 JavaBean等，这些操作都是由 HandlerApater来完成，开发者只需将注意力集中业务逻辑的处理上， DispatcherServlet通过 HandlerAdapter执行不同的 Handler。
      {: id="20210314232146-bwql796" updated="20210314232150"}
    - {: id="20210314232150-71jwdhc"}ModelAndview：装载了模型数据和视图信息，作为 Handler的处理结果，返回绐 Dispatcher Servlet。
      {: id="20210314232150-63mvaa0" updated="20210314232150"}
    - {: id="20210314235111-cip8h3u"}View Resolver：视图解析器， Dispatche Servlet通过它将逻辑视图解析为物理视图，最终将渲染结果响应给客户端
      {: id="20210314232317-rvrrjan" updated="20210314235110"}
    {: id="20210314235149-tzbzbam"}
  - {: id="20210314234854-9f0t2rn"}Spring MVc的工作流程
    {: id="20210314235111-hcf1apt"}

    - {: id="20210314235151-o4rwx3s"}客户端请求被 Disptacher Servlet接收
      {: id="20210314235151-cta10jz" updated="20210314235209"}
    - {: id="20210314235209-tdp8jsp"}根据 Handler Mapping映射到 Handler
      {: id="20210314235209-c5zalq3" updated="20210314235209"}
    - {: id="20210314235213-ndgd4bu"}生成 Handler和 HandlerInterceptor。
      {: id="20210314235213-z1bkrlh" updated="20210314235213"}
    - {: id="20210314235215-n685wzi"}Handler和 HandlerInterceptor以 Handler Execution Chain的形式一并返回给 Disptacher Servlet
      {: id="20210314235215-j59yyjs" updated="20210314235219"}
    - {: id="20210314235220-cwrqtns"}DispatcherServlet通过 HandlerAdapter调用 Handler的方法完成业务逻辑处理。
      {: id="20210314235220-x0dda3u" updated="20210314235223"}
    - {: id="20210314235223-cugd7lh"}Handler返回一个 ModelAndview给 DispatcherServlet
      {: id="20210314235223-6jvwgrq" updated="20210314235223"}
    - {: id="20210314235227-5h09cyf"}DispatcherServlet将获取的 ModelAndview对象传给 ViewResolver视图解析器，将逻辑视图解析为物理视图vew。
      {: id="20210314235227-s7qdwek" updated="20210314235235"}
    - {: id="20210314235236-76xa4au"}View Resovler返回一个vew给 DispatcherServlet DispatcherServlet根据view进行视图渲染（将模型数据Mode填充到视图vew中）。
      {: id="20210314235236-f35ofoh" updated="20210314235239"}
    - {: id="20210314235240-kau0yht"}DispatcherServlet将渲染后的结果响应给客户端
      {: id="20210314235240-tigsvip" updated="20210314235240"}

      ![image.png](assets/image-20210314233000-l7v83jx.png)
      {: id="20210314232956-efiu6ll" updated="20210314233000"}
    {: id="20210315085756-cmdgcp2"}
  - {: id="20210315085755-1zuoa7f"}Spring Mvc注解
    {: id="20210315085755-cu9muxl" updated="20210315085817"}

    - {: id="20210315085818-khjvsx9"}@RequestMapping
      {: id="20210315085818-qo1h2ei" updated="20210315085825"}

      - {: id="20210315085825-8lrnkyv"}Spring MVC通过@ RequestMapping注解将URL请求与业务方法进行映射，在 Handler的类定义处以及方法定义处都可以添加@ RequestMapping，在类定义处添加，相当于客户端多了一层访问路径
        {: id="20210315085825-5t4jg2m" updated="20210315085825"}
      {: id="20210315090004-rxyrb6q"}
    - {: id="20210315090003-jg8x3lk"}@Controller
      {: id="20210315090003-yykgeb9" updated="20210315090003"}

      - {: id="20210315090005-yzk4red"}@ Controller在类定义处添加，将该类交个loC容器来管理（结合 SpringMVC Xm的自动扫描配置使用），同时使其成为一个控制器，可以接收客户端请求
        {: id="20210315090005-ovlp1v2" updated="20210315090005"}
      {: id="20210315090120-8osfkz3"}
    - {: id="20210315090115-2n2tltu"}@ RequestMapping相关参数
      {: id="20210315090115-r4p9hx3" updated="20210315090135"}

      - {: id="20210315090135-ckec9m7"}value：指定URL请求的实际地址，是@ RequestMapping的默认值
        {: id="20210315090135-ccw0o1i" updated="20210315090207"}
      - {: id="20210315090208-q7tc4ry"}method：指定请求的 method类型，GET、PoST、PUT、 DELET
        {: id="20210315090208-xfvm3t2" updated="20210315090236"}
      - {: id="20210315090236-d8fbcbv"}params：指定请求中必须包含某些参数，否则无法调用该方法。
        {: id="20210315090236-qw9lr6r"}
      - {: id="20210315090950-etrz4ql"}关于参数绑定，在形参列表中通过添加@RequestParam注解完成HTTP请求参数与业务方法形参的映射。
        {: id="20210315090950-xbh9kap"}
      {: id="20210315091303-xpev268"}
    - {: id="20210315091249-qdir1xp"}Spring Mvc也支持 RESTFul风格的URL
      {: id="20210315091258-9c72u5q" updated="20210315091312"}

      - {: id="20210315091312-cvzsoof"}通过@ PathVariable注解完成请求参数与形参的映射
        {: id="20210315091528-06w86mv" updated="20210315093950"}
      {: id="20210315100600-70egqta"}
    - {: id="20210315093954-n95l0cl"}映射 Cookie
      {: id="20210315100356-jfbxcr6" updated="20210315100852"}

      - {: id="20210315100852-7phe1ob"}Spring Mvc通过映射可以直接在业务方法中获取 Cookie的值
        {: id="20210315100852-2ql140q" updated="20210315100911"}
      {: id="20210315100912-ql5fwxb"}
    - {: id="20210315100911-ipccq8w"}使用 JavaBean绑定参数
      {: id="20210315100911-97le5lf"}

      - {: id="20210315100927-jdyj62c"}Spring MVC会根据请求参数名和 JavaBean属性名进行自动匹配，自动为对象填充属性值，同时支持级联属性
        {: id="20210315100927-8guw98a" updated="20210315103215"}
      {: id="20210315103216-9arpriq"}
    - {: id="20210315103215-2nom1aq"}如果出现中文乱码问题，只需在 web. xm添加 Spring MVC自带的过滤器即可
      {: id="20210315103215-h17umm5" updated="20210315103308"}

      ```xml
      <filter>
          <filter-name>encodingFilter</filter-name>
          <filter-class>org. springframework web filter Character EncodingFilter</filter-class>
          <init-param>
              <param-name>encoding</param-name>
              <param-value>UTF-8</param-value>
          </init-param>
      </filter>
      <filter-mapping>
          <filter-name>encodingFilter</filter-name>
          <url-pattern>/*</url-pattern>
      </filter-mapping>
      ```
      {: id="20210315093613-u4tf4kn" updated="20210315103339"}
    - {: id="20210315103840-mdkjnbw"}JSP页面的转发和重定向
      {: id="20210315103840-i1mkkoz" updated="20210315103846"}

      - {: id="20210315103848-40ne3eu"}Spring Mvc默认是以转发的形式响应JSP
        {: id="20210315103848-n90lqnh" updated="20210315103853"}
      - {: id="20210315103854-n5evh1e"}转发：forward:
        {: id="20210315103854-n62ukqz" updated="20210315104851"}
      - {: id="20210315104018-r0589ml"}重定向：redirect:
        {: id="20210315104018-ozbu2w6" updated="20210315104858"}
      {: id="20210315104902-f11bd4y"}
    {: id="20210315105909-yg2qsod"}
  - {: id="20210315104902-va80o2i"}Spring Mvc数据绑定
    {: id="20210315104902-4kq3oia"}

    - {: id="20210315105933-di7zods"}数据绑定：在后端的业务方法中直接获取客户端HTP请求中的参数，将请求参数映射到业务方法的形参中， Spring Mvc中数据绑定的工作是由 HandlerAdapter来完成的。
      {: id="20210315105933-35ngg5q" updated="20210315105933"}
    - {: id="20210315110052-nagd1js"}@Response Body表示 Spring MvC会直接将业务方法的返回值响应给客户端，如果不加@ Response Body注解， Spring Mvc会将业务方法的放回值传递给 DispatcherServlet，再由 DisptacherServlet调用 ViewResolver对返回值进行解析，映射到一个JSP资源
      {: id="20210315110052-h5f5fyp" updated="20210315110103"}
    - {: id="20210315110820-b5qe6f0"}包装类
      {: id="20210315110820-dr2hawv"}

      - {: id="20210315110853-zma3ppz"}可以接收nul，当HTTP请求没有参数时，使用包装类定义形参的数据类型，程序不会抛出异常
        {: id="20210315110853-tlwze4x" updated="20210315110853"}
      - {: id="20210315110910-lcegk6b"}@RequestParam
        {: id="20210315110910-uhata99" updated="20210315110915"}

        - {: id="20210315110915-b9ihv99"}value="num"：将HTTP请求中名为num的参数赋给形参id。
          {: id="20210315110915-lp0zrcx" updated="20210315110919"}
        - {: id="20210315110923-tu9z2yf"}equried：设置num是否为必填项，true表示必填， false表示非必填，可省略defaultValue=“0"：如果HTTP请求中没有num参数，默认值为0
          {: id="20210315110923-f838e7j" updated="20210315110923"}
        {: id="20210315112502-7czl7lj"}
      {: id="20210315112502-x6lc0kg"}
    {: id="20210315112502-c1xm3ey"}
  {: id="20210315112503-k056heq"}
- {: id="20210315112500-vjb7pt8"}### MyBatis
  {: id="20210315112500-2bvyd0h" updated="20210315112525"}

  - {: id="20210315112527-tg0auw5"}My Batis概述
    {: id="20210315112527-lwjxl8o"}

    - {: id="20210315112551-mj1v652"}MyBatis是 apache的一个开源项目 iBatis，，2010年这个项目由 apache software foundation迁移到了 Google code，并且改名为 My Batis，2013年11月迁移到GitHub。
      {: id="20210315112551-jdvzis3" updated="20210315112551"}
    - {: id="20210315112556-dlmeo0u"}My Batis是一个实现了数据持久化的开源框架，简单理解就是对」DBC进行封装
      {: id="20210315112556-xcjg3k3" updated="20210315112556"}
    {: id="20210315112905-wzq8rj4"}
  - {: id="20210315112903-ylgfcpp"}ORMapping:Object Relationship Mapping
    {: id="20210315112903-f0ml21x"}

    - {: id="20210315112911-u349nel"}对象关系映射
      {: id="20210315112911-ozb6475" updated="20210315112911"}
    - {: id="20210315112915-vlibp9i"}对象指面向对象关
      {: id="20210315112915-k3v5b6g" updated="20210315112915"}
    - {: id="20210315112917-tjj8lqp"}系指关系型数据库
      {: id="20210315112917-y4nr41z" updated="20210315112917"}
    - {: id="20210315112919-1wbyfmd"}Java到 MySQLI的映射，开发者可以以面向对象的思想来管理数据库
      {: id="20210315112919-q74qjzm" updated="20210315112919"}
    {: id="20210315112912-04l8llc"}
  - {: id="20210315112606-q852c1w"}My Batis的优点
    {: id="20210315112606-nzb5xzj"}

    - {: id="20210315112716-k3hm6vu"}与JDB相比，减少了50%以上的代码量。
      {: id="20210315112716-174kluq" updated="20210315112716"}
    - {: id="20210315112723-g56q2sf"}MyBatis是最简单的持久化框架，小巧并且简单易学
      {: id="20210315112723-vuqokd2" updated="20210315112723"}
    - {: id="20210315112726-23lkt0s"}MyBatis相当灵活，不会对应用程序或者数据库的现有设计强加任何影响， SQL写在XML里，从程序代码中彻底分离，降低耦合度，便于统一管理和优化，并可重用。
      {: id="20210315112726-yfuxi94" updated="20210315112749"}
    - {: id="20210315112749-951bkiw"}提供XML标签，支持编写动态SQL语句。
      {: id="20210315112749-48lhm1r" updated="20210315112749"}
    - {: id="20210315112754-ehws8v0"}提供映射标签，支持对象与数据库的ORM字段关系映射。
      {: id="20210315112754-x84xhl3" updated="20210315112754"}
    {: id="20210315113058-wjf6srv"}
  - {: id="20210315113057-dhgmcst"}My Batis的缺点
    {: id="20210315113057-8pvtiei"}

    - {: id="20210315113131-qhg2mwp"}SQL语句的编写工作量较大，尤其是字段多、关联表多时，更是如此，对开发人员编写SQL语句的功底有一定要求
      {: id="20210315113131-sazl1us" updated="20210315113131"}
    - {: id="20210315113134-iyi54mn"}SL语句依赖于数握库，导致数据库移植性差，不能随意更换数据库
      {: id="20210315113134-i47ux72" updated="20210315113134"}
    {: id="20210315114402-l0hpdnf"}
  - {: id="20210315114400-3gpqc6e"}使用原生接口
    {: id="20210315114400-li5ugs9"}

    - {: id="20210315114417-ha4r9za"}My Batis框架需要开发者自定义SQL语句，写在 Mapper.xm文件中，实际开发中，会为每个实体类创建对应的Mapper.xm，定义管理该对象数据的SQL。
      {: id="20210315114417-cpm5ckq" updated="20210315114417"}
    - {: id="20210315114429-rulhqoe"}namespace通常设置为文件所在包+文件名的形式。
      {: id="20210315114429-8f94y3q"}
    - {: id="20210315114434-r8ht21k"}insert标签表示执行添加操作
      {: id="20210315114434-2wvv6zg" updated="20210315114435"}
    - {: id="20210315114443-0wc2cxj"}select标签表示执行查询操作
      {: id="20210315114443-r8brcst" updated="20210315114443"}
    - {: id="20210315114446-5rounjz"}update标签表示执行更新操作。
      {: id="20210315114446-xzsxbg4" updated="20210315114446"}
    - {: id="20210315114448-qj6mh12"}delete标签表示执行删除操作。
      {: id="20210315114448-0fko96n" updated="20210315114448"}
    - {: id="20210315114450-hkfpvio"}id是实际调用 My Batis方法时需要用到的参数
      {: id="20210315114450-t4qs8xd" updated="20210315114450"}
    - {: id="20210315114456-ma93q6n"}parameterType是调用对应方法时参数的数据类型。
      {: id="20210315114456-w1h53f5" updated="20210315114456"}
    {: id="20210315120403-7ibfuiw"}
  - {: id="20210315115037-ywgmnk1"}创建接口对应的 Mapper.xm，定义接口方法对应的SQL语句。
    {: id="20210315115037-hxmyzcg" updated="20210315120429"}

    - {: id="20210315120432-p9chitm"}statement标签可根据SQL执行的业务选择 Insert、 delete、 update、 select My Batis框架会根据规则自动创建接口实现类的代理对象规则
      {: id="20210315120432-k31hdxt" updated="20210315120436"}
    - {: id="20210315120437-ggupjkg"}Mapper.xml中 namespace为接口的全类名。
      {: id="20210315120437-afsv5at" updated="20210315120454"}
    - {: id="20210315120439-41kof78"}Mapper.xml中 statement的id为接口中对应的方法名。
      {: id="20210315120439-570jo34" updated="20210315120456"}
    - {: id="20210315120442-4zb5zes"}Mapper.xml中 statement的 parameterType和接口中对应方法的参数类型一致
      {: id="20210315120442-5btgw1x" updated="20210315120457"}
    - {: id="20210315120444-yp2svwm"}Mapper.xml中 statement的 resultType和接口中对应方法的返回值类型一致<123>
      {: id="20210315120444-8n36zbp" updated="20210315183924"}
    {: id="20210315120433-vbdano2"}
  {: id="20210315112527-xlonle1"}
{: id="20210314215524-s1vmtw8" updated="20210319180931"}

{: id="20210315103537-rwcvtyv"}


{: id="20210314215524-0qa1um9" type="doc"}
