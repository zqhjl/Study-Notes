镜像作为 Docker 三大核心概念中，最重要的一个关键词，它有很多操作，是您想学习容器技术不得不掌握的。本文将带您一步一步，图文并重，上手操作来学习它。
{: id="20210330211657-reo73xw"}

### 目录
{: id="20210330211657-fr532xi"}

<!-- TOC -->

- {: id="20210330211657-l22ldva"}[一 Docker 下载镜像](#一-docker-下载镜像)
  {: id="20210330211657-j3z3ebm"}
  - {: id="20210330211657-u9uwvzy"}[1.1 下载镜像](#11-下载镜像)
    {: id="20210330211657-xtxjk4l"}
  - {: id="20210330211657-yzv1gsq"}[1.2 验证](#12-验证)
    {: id="20210330211657-kaib2g0"}
  - {: id="20210330211657-o4rzh42"}[1.3 下载镜像相关细节](#13-下载镜像相关细节)
    {: id="20210330211657-zvhmp91"}
  - {: id="20210330211657-zbx7h5l"}[1.4 PULL 子命令](#14-pull-子命令)
    {: id="20210330211657-iyfn277"}
  {: id="20210330211657-2k6t8py"}
- {: id="20210330211657-th7ooxx"}[二 Docker 查看镜像信息](#二-docker-查看镜像信息)
  {: id="20210330211657-7pp2dx9"}
  - {: id="20210330211657-n6p6sow"}[2.1 images 命令列出镜像](#21-images-命令列出镜像)
    {: id="20210330211657-12ycq3y"}
  - {: id="20210330211657-ux1q5hl"}[2.2 使用 tag 命令为镜像添加标签](#22-使用-tag-命令为镜像添加标签)
    {: id="20210330211657-yhn81rv"}
  - {: id="20210330211657-o7bokt5"}[2.3 使用 inspect 命令查看镜像详细信息](#23-使用-inspect-命令查看镜像详细信息)
    {: id="20210330211657-jhz6k1l"}
  - {: id="20210330211657-e6r1jw2"}[2.4 使用 history 命令查看镜像历史](#24-使用-history-命令查看镜像历史)
    {: id="20210330211657-xn4zzhf"}
  {: id="20210330211657-54c9wd1"}
- {: id="20210330211657-o5hxt9z"}[三 Docker 搜索镜像](#三-docker-搜索镜像)
  {: id="20210330211657-b0z4mlg"}
  - {: id="20210330211657-zw8as7p"}[3.1 search 命令](#31-search-命令)
    {: id="20210330211657-lptst1l"}
  - {: id="20210330211657-gudqb8f"}[3.2 search 子命令](#32-search-子命令)
    {: id="20210330211657-2t29bvt"}
  {: id="20210330211657-54sxoqf"}
- {: id="20210330211657-e5jdmp9"}[四 Docker 删除镜像](#四-docker-删除镜像)
  {: id="20210330211657-nrw4rwd"}
  - {: id="20210330211657-l71uln4"}[4.1 通过标签删除镜像](#41-通过标签删除镜像)
    {: id="20210330211657-egkqwsk"}
  - {: id="20210330211657-ensxfoc"}[4.2 通过 ID 删除镜像](#42-通过-id-删除镜像)
    {: id="20210330211657-vi199s4"}
  - {: id="20210330211657-1qm6cz9"}[4.3 删除镜像的限制](#43-删除镜像的限制)
    {: id="20210330211657-wawq96k"}
  - {: id="20210330211657-vkrgjzp"}[4.4 清理镜像](#44-清理镜像)
    {: id="20210330211657-7gh7o6f"}
  {: id="20210330211657-ax7jzp0"}
- {: id="20210330211657-flf7gur"}[五 Docker 创建镜像](#五-docker-创建镜像)
  {: id="20210330211657-0rzdyq8"}
  - {: id="20210330211657-gk0jwyk"}[5.1 基于已有的镜像创建](#51-基于已有的镜像创建)
    {: id="20210330211657-jq9m9tg"}
  - {: id="20210330211657-yedgkvz"}[5.2 基于 Dockerfile 创建](#52-基于-dockerfile-创建)
    {: id="20210330211657-nll7v2a"}
  {: id="20210330211657-ystuhb8"}
- {: id="20210330211657-widp82e"}[六 Docker 导出&加载镜像](#六-docker-导出加载镜像)
  {: id="20210330211657-i5klu9c"}
  - {: id="20210330211657-73ireu1"}[6.1 导出镜像](#61-导出镜像)
    {: id="20210330211657-werxc89"}
  - {: id="20210330211657-xup0ump"}[6.2 加载镜像](#62-加载镜像)
    {: id="20210330211657-qhgqsl4"}
  {: id="20210330211657-wwnzfck"}
- {: id="20210330211657-1e4hwhh"}[七 Docker 上传镜像](#七-docker-上传镜像)
  {: id="20210330211657-xd8yqug"}
  - {: id="20210330211657-45zkevg"}[7.1 获取 Docker ID](#71-获取-docker-id)
    {: id="20210330211657-6tyvyh4"}
  - {: id="20210330211657-sfugjtd"}[7.2 创建镜像仓库](#72-创建镜像仓库)
    {: id="20210330211657-lilz3yh"}
  - {: id="20210330211657-7qx09vi"}[7.3 上传镜像](#73-上传镜像)
    {: id="20210330211657-seu828m"}
  {: id="20210330211657-duo5xfi"}
- {: id="20210330211657-xm1k08o"}[八 总结](#八-总结)
  {: id="20210330211657-c574yc0"}
{: id="20210330211657-ha3t4tb"}

<!-- /TOC -->

## 一 Docker 下载镜像
{: id="20210330211657-qe7kz3g"}

如果我们想要在本地运行容器，就必须保证本地存在对应的镜像。所以，第一步，我们需要下载镜像。当我们尝试下载镜像时，Docker 会尝试先从默认的镜像仓库（默认使用 Docker Hub 公共仓库）去下载，当然了，用户也可以自定义配置想要下载的镜像仓库。
{: id="20210330211657-zom278f"}

### 1.1 下载镜像
{: id="20210330211657-9af7eeo"}

镜像是运行容器的前提，我们可以使用 `docker pull[IMAGE_NAME]:[TAG]`命令来下载镜像，其中 `IMAGE_NAME` 表示的是镜像的名称，而 `TAG` 是镜像的标签，也就是说我们需要通过 “**镜像 + 标签**” 的方式来下载镜像。
{: id="20210330211657-2q4ixi3"}

**注意：** 您也可以不显式地指定 TAG, 它会默认下载 latest 标签，也就是下载仓库中最新版本的镜像。这里并不推荐您下载 latest 标签，因为该镜像的内容会跟踪镜像的最新版本，并随之变化，所以它是不稳定的。在生产环境中，可能会出现莫名其妙的 bug, 推荐您最好还是显示的指定具体的 TAG。
{: id="20210330211657-eh8joa8"}

举个例子，如我们想要下载一个 Mysql 5.7 镜像，可以通过命令来下载：
{: id="20210330211657-v0mpfac"}

```
docker pull mysql:5.7
```
{: id="20210330211657-a0lzt45"}

会看到控制台输出内容如下：
{: id="20210330211657-j1r7fnb"}

![Docker 下载镜像](https://mmbiz.qpic.cn/mmbiz_jpg/knmrNHnmCLHC3QNcSiaib3u3EM014CpBTPaaGfBRjupMm7dg74uP4a4jx1QeMY7PAHmqjFRYMkbsiaY0hZV3371uw/?wx_fmt=jpeg)
{: id="20210330211657-qgjoua7"}

**注意：** 由于官方 DockerHub 仓库服务器在国外，下载速度较慢，所以我将仓库的地址更改成了国内的 `docker.io` 的镜像仓库，所以在上图中，镜像前面会有 `docker.io` 出现。
{: id="20210330211657-mwpet75"}

当有 **Downloaded** 字符串输出的时候，说明下载成功了！！
{: id="20210330211657-uvgv3wm"}

### 1.2 验证
{: id="20210330211657-l8ovtge"}

让我们来验证一下，本地是否存在 Mysql5.7 的镜像，运行命令：
{: id="20210330211657-lo3uai4"}

```
docker images
```
{: id="20210330211657-stis119"}

![验证本地镜像是否存在](https://mmbiz.qpic.cn/mmbiz_jpg/knmrNHnmCLHC3QNcSiaib3u3EM014CpBTP0QbqA4STORwmkmv1OcZM8n8BiarCrWxGiayXFdMVGlvGjv7NUFNDWpHQ/?wx_fmt=jpeg)
{: id="20210330211657-uhi2ncr"}

可以看到本地的确存在该镜像，确实是下载成功了！
{: id="20210330211657-y3ijrps"}

### 1.3 下载镜像相关细节
{: id="20210330211657-unlc3b6"}

再说说上面下载镜像的过程：
{: id="20210330211657-6nzdq3a"}

![Docker 镜像下载](https://mmbiz.qpic.cn/mmbiz_jpg/knmrNHnmCLHC3QNcSiaib3u3EM014CpBTPKgsXuhayxmKjVSb5kkEB0ffKjUq2TB0FLA0Tqu7kIibRiawRP0afUcVA/?wx_fmt=jpeg)
{: id="20210330211657-lo01g2d"}

通过下载过程，可以看到，一个镜像一般是由多个层（ `layer`） 组成，类似 `f7e2b70d04ae`这样的串表示层的唯一 ID（实际上完整的 ID 包括了 256 个 bit, 64 个十六进制字符组成）。
{: id="20210330211657-yyisy06"}

**您可能会想，如果多个不同的镜像中，同时包含了同一个层（ layer）,这样重复下载，岂不是导致了存储空间的浪费么?**
{: id="20210330211657-i7xyujh"}

实际上，Docker 并不会这么傻会去下载重复的层（ `layer`）,Docker 在下载之前，会去检测本地是否会有同样 ID 的层，如果本地已经存在了，就直接使用本地的就好了。
{: id="20210330211657-htdnmuz"}

**另一个问题，不同仓库中，可能也会存在镜像重名的情况发生, 这种情况咋办？**
{: id="20210330211657-i3misnf"}

严格意义上，我们在使用 `docker pull` 命令时，还需要在镜像前面指定仓库地址( `Registry`), 如果不指定，则 Docker 会使用您默认配置的仓库地址。例如上面，由于我配置的是国内 `docker.io` 的仓库地址，我在 `pull` 的时候，docker 会默认为我加上 `docker.io/library` 的前缀。
{: id="20210330211657-lddpanr"}

如：当我执行 `docker pull mysql:5.7` 命令时，实际上相当于 `docker pull docker.io/mysql:5.7`，如果您未自定义配置仓库，则默认在下载的时候，会在镜像前面加上 DockerHub 的地址。
{: id="20210330211657-zjpji83"}

Docker 通过前缀地址的不同，来保证不同仓库中，重名镜像的唯一性。
{: id="20210330211657-xnhf7nm"}

### 1.4 PULL 子命令
{: id="20210330211657-r5mn708"}

命令行中输入：
{: id="20210330211657-qu13fhz"}

```
docker pull --help
```
{: id="20210330211657-3l7n202"}

会得到如下信息：
{: id="20210330211657-4pd9324"}

```
[root@iZbp1j8y1bab0djl9gdp33Z ~]# docker pull --help
Usage:  docker pull [OPTIONS] NAME[:TAG|@DIGEST]
Pull an image or a repository from a registry
Options:  -a, --all-tags                Download all tagged images in the repository      --disable-content-trust   Skip image verification (default true)      --help                    Print usage
```
{: id="20210330211657-009m07g"}

我们可以看到主要支持的子命令有：
{: id="20210330211657-t0guj1w"}

1. {: id="20210330211657-4rwn37j"}`-a,--all-tags=true|false`: 是否获取仓库中所有镜像，默认为否；
   {: id="20210330211657-7c2gnr0"}
2. {: id="20210330211657-cohfejs"}`--disable-content-trust`: 跳过镜像内容的校验，默认为 true;
   {: id="20210330211657-3qwx6he"}
{: id="20210330211657-7okuqyw"}

## 二 Docker 查看镜像信息
{: id="20210330211657-mpk1ve6"}

### 2.1 images 命令列出镜像
{: id="20210330211657-oyok9zn"}

通过使用如下两个命令，列出本机已有的镜像：
{: id="20210330211657-1znp1kl"}

```
docker images
```
{: id="20210330211657-3e1vx0n"}

或：
{: id="20210330211657-stzma5e"}

```
docker image ls
```
{: id="20210330211657-f61cxjw"}

如下图所示：
{: id="20210330211657-98h4f3i"}

![Docker 查看镜像信息](https://mmbiz.qpic.cn/mmbiz_jpg/knmrNHnmCLHC3QNcSiaib3u3EM014CpBTPo7bVaeYBiajiaZdfIN4J4D10WJ04W2zicZouiceKlDUbbte216HpCgErmQ/?wx_fmt=jpeg)
{: id="20210330211657-tksthyp"}

对上述红色标注的字段做一下解释：
{: id="20210330211657-mh4rkrv"}

- {: id="20210330211657-o5yxb8a"}**REPOSITORY**: 来自于哪个仓库；
  {: id="20210330211657-r1n83lb"}
- {: id="20210330211657-ag1x164"}**TAG**: 镜像的标签信息，比如 5.7、latest 表示不同的版本信息；
  {: id="20210330211657-sw42v8z"}
- {: id="20210330211657-cy6pcw2"}**IMAGE ID**: 镜像的 ID, 如果您看到两个 ID 完全相同，那么实际上，它们指向的是同一个镜像，只是标签名称不同罢了；
  {: id="20210330211657-v4z1xsc"}
- {: id="20210330211657-682623j"}**CREATED**: 镜像最后的更新时间；
  {: id="20210330211657-19zhvdn"}
- {: id="20210330211657-i9gxmrz"}**SIZE**: 镜像的大小，优秀的镜像一般体积都比较小，这也是我更倾向于使用轻量级的 alpine 版本的原因；
  {: id="20210330211657-5o8ybj3"}
{: id="20210330211657-2r8c6v3"}

> 注意：图中的镜像大小信息只是逻辑上的大小信息，因为一个镜像是由多个镜像层（ `layer`）组成的，而相同的镜像层本地只会存储一份，所以，真实情况下，占用的物理存储空间大小，可能会小于逻辑大小。
> {: id="20210330211657-bxobmbe"}
{: id="20210330211657-f8ivaqn"}

### 2.2 使用 tag 命令为镜像添加标签
{: id="20210330211657-oth7q4t"}

通常情况下，为了方便在后续工作中，快速地找到某个镜像，我们可以使用 `docker tag` 命令，为本地镜像添加一个新的标签。如下图所示：
{: id="20210330211657-yr9xzn8"}

![Docker tag 添加标签](https://mmbiz.qpic.cn/mmbiz_jpg/knmrNHnmCLHC3QNcSiaib3u3EM014CpBTPD2huWAicJUMBNZhf56OHXa0KjiaF2XcUvxyMm3mssibKvKa5UayFcD1WQ/?wx_fmt=jpeg)
{: id="20210330211657-75qqivd"}

为 `docker.io/mysql` 镜像，添加新的镜像标签 `allen_mysql:5.7`。然后使用 `docker images` 命令，查看本地镜像：
{: id="20210330211657-1ghsbja"}

![Docker tag 添加标签](https://mmbiz.qpic.cn/mmbiz_jpg/knmrNHnmCLHC3QNcSiaib3u3EM014CpBTPCDq6MvlhsiawBwhNn7OEwJassCnwjibP4gWwqAvG3xow9LwFf2ticUsdg/?wx_fmt=jpeg)
{: id="20210330211657-bg8ao1p"}

可以看到，本地多了一个 `allen_mysql:5.7` 的镜像。细心的你一定还会发现， `allen_mysql:5.7` 和 `docker.io/mysql:5.7` 的镜像 ID 是一模一样的，说明它们是同一个镜像，只是别名不同而已。
{: id="20210330211657-1hk5ge8"}

`docker tag` 命令功能更像是, 为指定镜像添加快捷方式一样。
{: id="20210330211657-0e5v5ry"}

### 2.3 使用 inspect 命令查看镜像详细信息
{: id="20210330211657-7pt7yo5"}

通过 `docker inspect` 命令，我们可以获取镜像的详细信息，其中，包括创建者，各层的数字摘要等。
{: id="20210330211657-v8lk8kn"}

```
docker inspect docker.io/mysql:5.7
```
{: id="20210330211657-80xpkat"}

![Docker inspect 查看镜像详细信息](https://mmbiz.qpic.cn/mmbiz_jpg/knmrNHnmCLHC3QNcSiaib3u3EM014CpBTPzL9a3cEkXSh4uuSSwia4pibNjT4dDV7t1AgFuJkrBAq3CkU2WWorEFdg/?wx_fmt=jpeg)
{: id="20210330211657-fj3dwox"}

`docker inspect` 返回的是 `JSON` 格式的信息，如果您想获取其中指定的一项内容，可以通过 `-f` 来指定，如获取镜像大小：
{: id="20210330211657-4t1apke"}

```
docker inspect -f {{".Size"}} docker.io/mysql:5.7
```
{: id="20210330211657-wacwse2"}

![Docker inspect 查看镜像详细信息](https://mmbiz.qpic.cn/mmbiz_jpg/knmrNHnmCLHC3QNcSiaib3u3EM014CpBTPsa7t1OSDhWgFxEzCdfyNaOduGmsz7xJEobUZFibzw5UFxmKvrcmwGNA/?wx_fmt=jpeg)
{: id="20210330211657-qolvi87"}

### 2.4 使用 history 命令查看镜像历史
{: id="20210330211657-ya35evw"}

前面的小节中，我们知道了，一个镜像是由多个层（layer）组成的，那么，我们要如何知道各个层的具体内容呢？
{: id="20210330211657-qwp9mhq"}

通过 `docker history` 命令，可以列出各个层（layer）的创建信息，如我们查看 `docker.io/mysql:5.7` 的各层信息：
{: id="20210330211657-2ejpt7a"}

```
docker history docker.io/mysql:5.7
```
{: id="20210330211657-awc4b84"}

![Docker history 各层信息](https://mmbiz.qpic.cn/mmbiz_jpg/knmrNHnmCLHC3QNcSiaib3u3EM014CpBTPQ8F21nmOQ7RLI5ibAgVpcOkBlIRR2kH4B0VlDExiauskHbE0w0HYeE0w/?wx_fmt=jpeg)
{: id="20210330211657-1zvteod"}

可以看到，上面过长的信息，为了方便展示，后面都省略了，如果您想要看具体信息，可以通过添加 `--no-trunc` 选项，如下面命令：
{: id="20210330211657-t4kr1bi"}

```
docker history --no-trunc docker.io/mysql:5.7
```
{: id="20210330211657-fphdtiy"}

## 三 Docker 搜索镜像
{: id="20210330211657-tu1e46x"}

### 3.1 search 命令
{: id="20210330211657-m98jann"}

您可以通过下面命令进行搜索：
{: id="20210330211657-4a33wse"}

```
docker search [option] keyword
```
{: id="20210330211657-cxph2th"}

比如，您想搜索仓库中 `mysql` 相关的镜像，可以输入如下命令：
{: id="20210330211657-d5mbgmp"}

```
docker search mysql
```
{: id="20210330211657-5jkp1rj"}

![Docker 搜索镜像](https://mmbiz.qpic.cn/mmbiz_jpg/knmrNHnmCLHC3QNcSiaib3u3EM014CpBTP3PBGU7q2NoK6WGSRmcxWs0OMicjeDwTBFvOAbXB5MuaDFPYXAod3NZA/?wx_fmt=jpeg)
{: id="20210330211657-w9jrwf4"}

### 3.2 search 子命令
{: id="20210330211657-f4zfp6l"}

命令行输入 `docker search --help`, 输出如下：
{: id="20210330211657-788d3i9"}

```
Usage:  docker search [OPTIONS] TERM
Search the Docker Hub for images
Options:  -f, --filter filter   Filter output based on conditions provided      --help            Print usage      --limit int       Max number of search results (default 25)      --no-index        Don't truncate output      --no-trunc        Don't truncate output
```
{: id="20210330211657-0drxt4e"}

可以看到 `search` 支持的子命令有：
{: id="20210330211657-qtwk17r"}

- {: id="20210330211657-ica9w90"}`-f,--filter filter`: 过滤输出的内容；
  {: id="20210330211657-tacgnbu"}
- {: id="20210330211657-8mvd3ii"}`--limitint`：指定搜索内容展示个数;
  {: id="20210330211657-tyn438h"}
- {: id="20210330211657-nmyyggf"}`--no-index`: 不截断输出内容；
  {: id="20210330211657-ejorh22"}
- {: id="20210330211657-556fy70"}`--no-trunc`：不截断输出内容；
  {: id="20210330211657-ixmdhi3"}
{: id="20210330211657-i6wwrkw"}

举个列子，比如我们想搜索官方提供的 mysql 镜像，命令如下：
{: id="20210330211657-15nf5y4"}

```
docker search --filter=is-official=true mysql
```
{: id="20210330211657-6mrkff1"}

![Docker 搜索官方镜像](https://mmbiz.qpic.cn/mmbiz_jpg/knmrNHnmCLHC3QNcSiaib3u3EM014CpBTPup8t50skwCOEX0pwnR9uicvWZWNxc7Vv4slXzIoGLhSPcwDq51xpUGA/?wx_fmt=jpeg)
{: id="20210330211657-nibo5qj"}

再比如，我们想搜索 Stars 数超过 100 的 mysql 镜像：
{: id="20210330211657-anfdh4y"}

```
docker search --filter=stars=100 mysql
```
{: id="20210330211657-yapkd4k"}

![Docker 搜索镜像](https://mmbiz.qpic.cn/mmbiz_jpg/knmrNHnmCLHC3QNcSiaib3u3EM014CpBTPsbeMVBSiaLLINzVmkbG3VtIbr3XJnVbIqWKvS016Yib3WQQmraqlENGA/?wx_fmt=jpeg)
{: id="20210330211657-zu26cgg"}

## 四 Docker 删除镜像
{: id="20210330211657-1vsrldb"}

### 4.1 通过标签删除镜像
{: id="20210330211657-wmj2se9"}

通过如下两个都可以删除镜像：
{: id="20210330211657-mzexiix"}

```
docker rmi [image]
```
{: id="20210330211657-lrtej0z"}

或者：
{: id="20210330211657-58ltj2n"}

```
docker image rm [image]
```
{: id="20210330211657-hj5gjb1"}

支持的子命令如下：
{: id="20210330211657-ocxfttq"}

- {: id="20210330211657-2ha0yy8"}`-f,-force`: 强制删除镜像，即便有容器引用该镜像；
  {: id="20210330211657-7t6xoqv"}
- {: id="20210330211657-nl49nsr"}`-no-prune`: 不要删除未带标签的父镜像；
  {: id="20210330211657-wr2ojkm"}
{: id="20210330211657-s3j6o48"}

![Docker 查看镜像信息](https://mmbiz.qpic.cn/mmbiz_jpg/knmrNHnmCLFSKI1RxMqyrVlVX4GRveHHjMP3NiaSibZZ0XKTiasurB1giae3nfZvWZibRal7TKfiaAhJicXQfibicqCo5Kw/?wx_fmt=jpeg)Docker 查看镜像信息
{: id="20210330211657-52qyiz0"}

例如，我们想删除上章节创建的 `allen_mysql:5.7` 镜像，命令如下：
{: id="20210330211657-eedfip3"}

```shell
docker rmi allen_mysql:5.7
```
{: id="20210330211657-62jfhfa"}

![Docker 删除镜像](https://mmbiz.qpic.cn/mmbiz_jpg/knmrNHnmCLFSKI1RxMqyrVlVX4GRveHHfh5oDc3GDzlp7B5oaVRic7hHIzvRicDz1wCbgIBrQvMXK8jYo3yPOl5Q/?wx_fmt=jpeg)
{: id="20210330211657-uap5hhy"}

从上面章节中，我们知道 `allen_mysql:5.7` 和 `docker.io/mysql:5.7` 实际上指向的是同一个镜像，那么，您可以能会有疑问，我删除了 `allen_mysql:5.7`, 会不会将 `docker.io/mysql:5.7` 镜像也给删除了？
{: id="20210330211657-t7umjfh"}

**实际上，当同一个镜像拥有多个标签时，执行 `docker rmi` 命令，只是会删除了该镜像众多标签中，您指定的标签而已，并不会影响原始的那个镜像文件。**
{: id="20210330211657-dz04i17"}

不信的话，我们可以执行 `docker images` 命令，来看下 `docker.io/mysql:5.7` 镜像还在不在：
{: id="20210330211657-uf6s2mb"}

![Docker 查看镜像信息](https://mmbiz.qpic.cn/mmbiz_jpg/knmrNHnmCLFSKI1RxMqyrVlVX4GRveHHiciaqjoLKZiaoVZFeLJkfA2TfUKaib2muSNrTJP2Rvicib4ac3gMXPiaBkB9Q/?wx_fmt=jpeg)
{: id="20210330211657-hzzrh3t"}

可以看到， `docker.io/mysql:5.7` 镜像依然存在！
{: id="20210330211657-e359o4n"}

那么，如果某个镜像不存在多个标签，当且仅当只有一个标签时，执行删除命令时，您就要小心了，这会彻底删除镜像。
{: id="20210330211657-vk9a1mq"}

例如，这个时候，我们再执行 `docker rmi docker.io/mysql:5.7` 命令：
{: id="20210330211657-aaxob4c"}

![Docker 删除镜像](https://mmbiz.qpic.cn/mmbiz_jpg/knmrNHnmCLFSKI1RxMqyrVlVX4GRveHHAjqtv8JHovzTCdfIM5fIT5Nia3iaI7wKLo13vQgsWibRR9Y2Fd73V9czg/?wx_fmt=jpeg)
{: id="20210330211657-x4gkadg"}

从上图可以看到，我们已经删除了 `docker.io/mysql:5.7` 镜像的所有文件层。该镜像在本地已不复存在了！
{: id="20210330211657-lwr2nr9"}

### 4.2 通过 ID 删除镜像
{: id="20210330211657-jatzzdy"}

除了通过标签名称来删除镜像，我们还可以通过制定镜像 ID, 来删除镜像，如：
{: id="20210330211657-6owjr43"}

```
docker rmi ee7cbd482336
```
{: id="20210330211657-0v2bubq"}

一旦制定了通过 ID 来删除镜像，它会先尝试删除所有指向该镜像的标签，然后在删除镜像本身。
{: id="20210330211657-ngnlyxu"}

### 4.3 删除镜像的限制
{: id="20210330211657-1ky4y1w"}

删除镜像很简单，但也不是我们何时何地都能删除的，它存在一些限制条件。
{: id="20210330211657-chc24cl"}

当通过该镜像创建的容器未被销毁时，镜像是无法被删除的。为了验证这一点，我们来做个试验。首先，我们通过 `docker pull alpine` 命令，拉取一个最新的 `alpine` 镜像, 然后启动镜像，让其输出 `hello,docker!`:
{: id="20210330211657-6p4rzke"}

![Docker run alpine](https://mmbiz.qpic.cn/mmbiz_jpg/knmrNHnmCLFSKI1RxMqyrVlVX4GRveHHia157yicRQe5g5ad36peutDlAxuGcWbdxopEwmHXCM7rga80cYj0CguA/?wx_fmt=jpeg)
{: id="20210330211657-10rvwq0"}

接下来，我们来删除这个镜像试试：
{: id="20210330211657-jw5mmnf"}

![Docker 删除镜像](https://mmbiz.qpic.cn/mmbiz_jpg/knmrNHnmCLFSKI1RxMqyrVlVX4GRveHHia5wTHrVKT1NPHFZvLicwMicKibG5VHVjEWJOXrPOG4pK5VDwAYMcAYzJg/?wx_fmt=jpeg)
{: id="20210330211657-pg9mjx1"}

可以看到提示信息，无法删除该镜像，因为有容器正在引用他！同时，这段信息还告诉我们，除非通过添加 `-f` 子命令，也就是强制删除，才能移除掉该镜像！
{: id="20210330211657-of89dhe"}

```
docker rmi -f docker.io/alpine
```
{: id="20210330211657-45zovrp"}

但是，我们一般不推荐这样暴力的做法，正确的做法应该是：
{: id="20210330211657-xzmmryh"}

1. {: id="20210330211657-rej6imj"}先删除引用这个镜像的容器；
   {: id="20210330211657-s9jwv3m"}
2. {: id="20210330211657-c6a6wf7"}再删除这个镜像；
   {: id="20210330211657-92o5i2b"}
{: id="20210330211657-oqcza16"}

也就是，根据上图中提示的，引用该镜像的容器 ID ( `9d59e2278553`), 执行删除命令：
{: id="20210330211657-q3w9oka"}

```
docker rm 9d59e2278553
```
{: id="20210330211657-l95mm9o"}

然后，再执行删除镜像的命令：
{: id="20210330211657-l3gnbov"}

```
docker rmi 5cb3aa00f899
```
{: id="20210330211657-astax1n"}

![Docker 删除镜像](https://mmbiz.qpic.cn/mmbiz_jpg/knmrNHnmCLFSKI1RxMqyrVlVX4GRveHHWibytB1NGVzS1KBMia7sYMNm2eStNd4PicxoYA5CfQficMh4eoJMjtHiacA/?wx_fmt=jpeg)Docker 删除镜像
{: id="20210330211657-j9eanx6"}

这个时候，就能正常删除了！
{: id="20210330211657-4wlb2fz"}

### 4.4 清理镜像
{: id="20210330211657-of2ss61"}

我们在使用 Docker 一段时间后，系统一般都会残存一些临时的、没有被使用的镜像文件，可以通过以下命令进行清理：
{: id="20210330211657-9jrs7ce"}

```
docker image prune
```
{: id="20210330211657-ecnnps2"}

它支持的子命令有：
{: id="20210330211657-v8gfer9"}

- {: id="20210330211657-qvw9cvg"}`-a,--all`: 删除所有没有用的镜像，而不仅仅是临时文件；
  {: id="20210330211657-ag9w62j"}
- {: id="20210330211657-bf2e2bt"}`-f,--force`：强制删除镜像文件，无需弹出提示确认；
  {: id="20210330211657-q0ntdg8"}
{: id="20210330211657-fdwih54"}

## 五 Docker 创建镜像
{: id="20210330211657-504gugo"}

此小节中，您将学习 Docker 如何创建镜像？Docker 创建镜像主要有三种：
{: id="20210330211657-w3423lr"}

1. {: id="20210330211657-6t0i309"}基于已有的镜像创建；
   {: id="20210330211657-2g2278s"}
2. {: id="20210330211657-hxv81ck"}基于 Dockerfile 来创建；
   {: id="20210330211657-j2xbqk7"}
3. {: id="20210330211657-vsprokk"}基于本地模板来导入；
   {: id="20210330211657-qouom8o"}
{: id="20210330211657-n22z6vr"}

我们将主要介绍常用的 1，2 两种。
{: id="20210330211657-pfebnit"}

### 5.1 基于已有的镜像创建
{: id="20210330211657-qqaw7wh"}

通过如下命令来创建：
{: id="20210330211657-m0ghrd2"}

```
docker container commit
```
{: id="20210330211657-4qt1iyz"}

支持的子命令如下：
{: id="20210330211657-k9de3ct"}

- {: id="20210330211657-4qt7cqa"}`-a,--author`="": 作者信息；
  {: id="20210330211657-nflkiar"}
- {: id="20210330211657-zn1oh4e"}`-c,--change`=[]: 可以在提交的时候执行 Dockerfile 指令，如 CMD、ENTRYPOINT、ENV、EXPOSE、LABEL、ONBUILD、USER、VOLUME、WORIR 等；
  {: id="20210330211657-fkyx29a"}
- {: id="20210330211657-qg1u526"}`-m,--message`="": 提交信息；
  {: id="20210330211657-ftyirvw"}
- {: id="20210330211657-rg00vw1"}`-p,--pause`=true: 提交时，暂停容器运行。
  {: id="20210330211657-6qek9vo"}
{: id="20210330211657-w5okz9j"}

接下来，基于本地已有的 Ubuntu 镜像，创建一个新的镜像：
{: id="20210330211657-1xcq64q"}

![Docker 创建镜像](https://mmbiz.qpic.cn/mmbiz_jpg/knmrNHnmCLFSKI1RxMqyrVlVX4GRveHHMibkCiaNb1AbTNoQicVKkiaAOIhZO2FsRNbSY0kzqZezVGcfgOibJRD58QQ/?wx_fmt=jpeg)
{: id="20210330211657-ehdoc2a"}

首先，让我将它运行起来，并在其中创建一个 test.txt 文件：
{: id="20210330211657-arckcqu"}

![Docker 创建镜像](https://mmbiz.qpic.cn/mmbiz_jpg/knmrNHnmCLFSKI1RxMqyrVlVX4GRveHHQd7AuibW8ml35Tk90OO15s43CAHQtXx5kYzibP5vtNAwic95qibDza61BQ/?wx_fmt=jpeg)
{: id="20210330211657-zycstjv"}

命令如下：
{: id="20210330211657-u03m4fd"}

```
docker run -it docker.io/ubuntu:latest /bin/bashroot@a0a0c8cfec3a:/# touch test.txtroot@a0a0c8cfec3a:/# exit
```
{: id="20210330211657-jp9xby8"}

创建完 test.txt 文件后，需要记住标注的容器 ID: `a0a0c8cfec3a`, 用它来提交一个新的镜像(**PS: 你也可以通过名称来提交镜像，这里只演示通过 ID 的方式**)。
{: id="20210330211657-fmlgce0"}

执行命令：
{: id="20210330211657-qgjw892"}

```
docker container commit -m "Added test.txt file" -a "Allen" a0a0c8cfec3a test:0.1
```
{: id="20210330211657-ew0nhm3"}

提交成功后，会返回新创建的镜像 ID 信息，如下图所示：
{: id="20210330211657-c8hmjmf"}

![Docker 提交新创建的镜像](https://mmbiz.qpic.cn/mmbiz_jpg/knmrNHnmCLFSKI1RxMqyrVlVX4GRveHHgX5ks187yqupLWLQnvNuwLGibc6So1xk8OZc6SpXEVB5zDEo6WlxQhw/?wx_fmt=jpeg)
{: id="20210330211657-ky5nb5k"}

再次查看本地镜像信息，可以看到新创建的 `test:0.1` 镜像了：
{: id="20210330211657-0rtfeib"}

![Docker 查看镜像信息](https://mmbiz.qpic.cn/mmbiz_jpg/knmrNHnmCLFSKI1RxMqyrVlVX4GRveHHibWZE9BBMrgVAzDAbpWibEANicPohJErNVCQpAFMfvKExoLj2EQlIYQ2g/?wx_fmt=jpeg)
{: id="20210330211657-d63clv6"}

### 5.2 基于 Dockerfile 创建
{: id="20210330211657-3y5zrd0"}

通过 Dockerfile 的方式来创建镜像，是最常见的一种方式了，也是比较推荐的方式。Dockerfile 是一个文本指令文件，它描述了是如何基于一个父镜像，来创建一个新镜像的过程。
{: id="20210330211657-1k0gvae"}

下面让我们来编写一个简单的 Dockerfile 文件，它描述了基于 Ubuntu 父镜像，安装 Python3 环境的镜像：
{: id="20210330211657-6bx7sfc"}

```
FROM docker.io/ubuntu:latest
LABEL version="1.0" maintainer="Allen <weiwosuo@github>"
RUN apt-get update && \    apt-get install -y python3 && \    apt-get clean && \    rm -rf /var/lib/apt/lists/*
```
{: id="20210330211657-9j92wvi"}

创建完成后，通过这个 Dockerfile 文件，来构建新的镜像，执行命令：
{: id="20210330211657-pab3yhe"}

```
docker image build -t python:3 .
```
{: id="20210330211657-78quck4"}

**注意：** 命令的最后有个点，如果不加的话，会构建不成功 ！
{: id="20210330211657-dp8zful"}

![Docker 通过 Dockerfile 构建镜像](https://mmbiz.qpic.cn/mmbiz_jpg/knmrNHnmCLFSKI1RxMqyrVlVX4GRveHHk6rCexCL5PcQqMia6QzvOicMg754BKO3mOibQCfQ6MI7tR1JA2A5ZqI7A/?wx_fmt=jpeg)
{: id="20210330211657-p6vmgha"}

编译成功后，再次查看本地镜像信息，就可以看到新构建的 python:3 镜像了。
{: id="20210330211657-vjy5au0"}

![Docker 查看镜像信息](https://mmbiz.qpic.cn/mmbiz_jpg/knmrNHnmCLFSKI1RxMqyrVlVX4GRveHH0amjBEf1pRGNUS4SbzibupypIebmiarHLotk3s1n2PdaqUPibrEaSoTvQ/?wx_fmt=jpeg)
{: id="20210330211657-9kwzjrn"}

## 六 Docker 导出&加载镜像
{: id="20210330211657-x0do73y"}

此小节中，您将学习 Docker 如何导出&加载镜像。
{: id="20210330211657-rau4aga"}

通常我们会有下面这种需求，需要将镜像分享给别人，这个时候，我们可以将镜像导出成 tar 包，别人直接通过加载这个 tar 包，快速地将镜像引入到本地镜像库。
{: id="20210330211657-a8mi3e0"}

要想使用这两个功能，主要是通过如下两个命令：
{: id="20210330211657-rcgc5lc"}

1. {: id="20210330211657-e1qbb3k"}`docker save`
   {: id="20210330211657-i33fy3w"}
2. {: id="20210330211657-q0jo6o9"}`docker load`
   {: id="20210330211657-5jmgend"}
{: id="20210330211657-wqcsb74"}

### 6.1 导出镜像
{: id="20210330211657-9vir08a"}

查看本地镜像如下：
{: id="20210330211657-bln3rei"}

![Docker 查看镜像信息](https://mmbiz.qpic.cn/mmbiz_jpg/knmrNHnmCLFSKI1RxMqyrVlVX4GRveHH0amjBEf1pRGNUS4SbzibupypIebmiarHLotk3s1n2PdaqUPibrEaSoTvQ/?wx_fmt=jpeg)
{: id="20210330211657-kmg9mhc"}

例如，我们想要将 python:3 镜像导出来，执行命令：
{: id="20210330211657-5lm0rgj"}

```
docker save -o python_3.tar python:3
```
{: id="20210330211657-mgxsxa4"}

执行成功后，查看当前目录：
{: id="20210330211657-kxed0hh"}

![Docker 导出文件](https://mmbiz.qpic.cn/mmbiz_jpg/knmrNHnmCLFSKI1RxMqyrVlVX4GRveHHOzOhDgY43hbGSGena4g7YpYREdwD1pzWPanhic1pb0LmFrsNGKAYK8g/?wx_fmt=jpeg)Docker 导出文件
{: id="20210330211657-ki6rld4"}

可以看到 `python_3.tar` 镜像文件已经生成。接下来，你可以将它通过复制的方式，分享给别人了！
{: id="20210330211657-a9tslh6"}

### 6.2 加载镜像
{: id="20210330211657-576d5b5"}

别人拿到了这个 `tar` 包后，要如何导入到本地的镜像库呢？
{: id="20210330211657-pcek9r1"}

通过执行如下命令：
{: id="20210330211657-0ru7yuc"}

```
docker load -i python_3.tar
```
{: id="20210330211657-r061rzb"}

或者：
{: id="20210330211657-yn2vhfq"}

```
docker load < python_3.tar
```
{: id="20210330211657-hplgymf"}

导入成功后，查看本地镜像信息，你就可以获得别人分享的镜像了！怎么样，是不是很方便呢！
{: id="20210330211657-cr9esbe"}

## 七 Docker 上传镜像
{: id="20210330211657-8xqjwma"}

我们将以上传到 Docker Hub 上为示例，演示 Docker 如何上传镜像。
{: id="20210330211657-fbo4uca"}

### 7.1 获取 Docker ID
{: id="20210330211657-gob59zi"}

想要上传镜像到 Docker Hub 上，首先，我们需要注册 Docker Hub 账号。打开 Docker Hub 网址 https://hub.docker.com，开始注册：
{: id="20210330211657-6p6c4t5"}

![Docker Hub 注册账号](https://mmbiz.qpic.cn/mmbiz_jpg/knmrNHnmCLFSKI1RxMqyrVlVX4GRveHH6JticENibsia3hkfDDuBq7PtOotic7rPK46wFdotM0LUYuyFZbOVUaJoeQ/?wx_fmt=jpeg)
{: id="20210330211657-2zskivn"}

填写您的 Docker ID (也就是账号)，以及密码，Email, 点击继续。
{: id="20210330211657-c3690di"}

接下来，Docker Hub 会发送验证邮件，到您填写的邮箱当中：
{: id="20210330211657-szc0sas"}

![Docker Hub 验证邮件](https://mmbiz.qpic.cn/mmbiz_jpg/knmrNHnmCLFSKI1RxMqyrVlVX4GRveHHfedKcp34V4t351TqTfBiaRmwAbHmOnVadHydicp3MtLQnUykQYUV49FA/?wx_fmt=jpeg)
{: id="20210330211657-1e8nc8v"}

点击验证即可，接下来，再次返回 Docker Hub 官网，用您刚刚注册的 Docker ID 和密码来登录账号！
{: id="20210330211657-6z2dqe4"}

![Docker Hub 登录页面](https://mmbiz.qpic.cn/mmbiz_jpg/knmrNHnmCLFSKI1RxMqyrVlVX4GRveHHa5I17YSce16BNFOgNayA0iaWYWGJnHWwZUjslrBRyV1jLssDKa7mysA/?wx_fmt=jpeg)
{: id="20210330211657-ynuvz9s"}

### 7.2 创建镜像仓库
{: id="20210330211657-r8qusdi"}

登录成功后，会出现如下页面：
{: id="20210330211657-fcwxbg6"}

![欢迎来到 Docker Hub](https://mmbiz.qpic.cn/mmbiz_jpg/knmrNHnmCLFSKI1RxMqyrVlVX4GRveHHRI3SFiaSl2yuXXO1CLhRDR03mVpTO4jwmljIaZC0KptcW7kmM03Xxicg/?wx_fmt=jpeg)
{: id="20210330211657-1jentgx"}

选择创建一个镜像仓库：
{: id="20210330211657-fpmqw6l"}

![创建 Python 仓库](https://mmbiz.qpic.cn/mmbiz_jpg/knmrNHnmCLFSKI1RxMqyrVlVX4GRveHHMsc31Uskib3SRM4uZZCqkYwyNJFN8ia4LkAKNZuurAbHJyQ1fib9DKGEw/?wx_fmt=jpeg)
{: id="20210330211657-ly72b93"}

填写**仓库名称**、**描述信息**、**是否公开后**，点击创建。
{: id="20210330211657-1xg0buj"}

![仓库镜像展示页](https://mmbiz.qpic.cn/mmbiz_jpg/knmrNHnmCLFSKI1RxMqyrVlVX4GRveHH688icujdAHnPOcHEaATxupbOn4u7LSKEBKoDWb1dPISiaP757VBibdwGQ/?wx_fmt=jpeg)仓库镜像展示页
{: id="20210330211657-9lkrxh3"}

我们看到，仓库已经创建成功了，但是里面还没有任何镜像，接下来开始上传镜像，到此新创建的仓库中。
{: id="20210330211657-117ckek"}

### 7.3 上传镜像
{: id="20210330211657-ir29zbg"}

进入命令行，**用我们刚刚获取的 Docker ID 以及密码登录**，执行命令：
{: id="20210330211657-274fbuq"}

```
docker login
```
{: id="20210330211657-8bufqqe"}

![命令行登录 Docker ID](https://mmbiz.qpic.cn/mmbiz_jpg/knmrNHnmCLFSKI1RxMqyrVlVX4GRveHHsJNOaXDpy3C4vu3xPOQUA9XfYFiasZOs69PLOxpUSiaGvEicYib3WKm88Q/?wx_fmt=jpeg)命令行登录 Docker ID
{: id="20210330211657-a37r3s3"}

登录成功后，我们开始准备上传本地的 `python:3` 镜像：
{: id="20210330211657-4pnwx9z"}

![python:3 镜像](https://mmbiz.qpic.cn/mmbiz_jpg/knmrNHnmCLFSKI1RxMqyrVlVX4GRveHHNNakMbCH4TFQTT0iad9Eb2vde8JzfgwIXFLpiaKzeMAYIa7ft22wBMEA/?wx_fmt=jpeg)
{: id="20210330211657-8rac93k"}

首先，我们对其打一个新的标签，**前缀与我们新创建的 Docker ID 、仓库名保持一致**:
{: id="20210330211657-pyu09p1"}

```
docker tag python:3 weiwosuoai1991/python:3
```
{: id="20210330211657-pl7p6ap"}

![python:3 镜像打标签](https://mmbiz.qpic.cn/mmbiz_jpg/knmrNHnmCLFSKI1RxMqyrVlVX4GRveHHSl8ria0e1kFFWlI1gAwwszV28IkztLv0s9XSZG6ficYIAoO1mfo4LrmQ/?wx_fmt=jpeg)
{: id="20210330211657-u81v136"}

查看本地信息，可以看到，标签打成功了。接下开，开始上传！执行命令：
{: id="20210330211657-fewcotr"}

```
docker push weiwosuoai1991/python:3
```
{: id="20210330211657-f59tvia"}

![上传 python:3 镜像](https://mmbiz.qpic.cn/mmbiz_jpg/knmrNHnmCLFSKI1RxMqyrVlVX4GRveHHeiaV2FtSpv7ewkpyOLEo7e6No42GSbCLqfaxjUicnFhBEq7m4OyIR6GA/?wx_fmt=jpeg)
{: id="20210330211657-c5sbi7p"}

上传成功！去 Docker Hub 官网，新创建的仓库的信息页面验证一下，是否真的成功了：
{: id="20210330211657-8jmhyai"}

![仓库镜像展示页](https://mmbiz.qpic.cn/mmbiz_jpg/knmrNHnmCLFSKI1RxMqyrVlVX4GRveHH5ibFBuhibrBn6Xe9tgxgO7LxtXI9FJ0HtLjvuibJhBqZPyexWY78MmBiag/?wx_fmt=jpeg)仓库镜像展示页
{: id="20210330211657-vo5rfds"}

大工告成！！！
{: id="20210330211657-ppklo7l"}

## 八 总结
{: id="20210330211657-5ebnxj7"}

本文中，我们着重学习了 Docker 中下载镜像,、查看镜像信息、搜索镜像、删除镜像,、创建镜像、导出&加载镜像以及向 Docker Hub 上传镜像的相关操作。
{: id="20210330211657-6zbrro9"}


{: id="20210330211657-vyyhq7d" type="doc"}
