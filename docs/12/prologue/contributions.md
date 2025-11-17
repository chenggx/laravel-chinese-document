# 贡献指南

- [错误报告](#错误报告)
- [支持问题](#支持问题)
- [核心开发讨论](#核心开发讨论)
- [选择分支](#选择分支)
- [编译资源](#编译资源)
- [安全漏洞](#安全漏洞)
- [编码风格](#编码风格)
    - [PHPDoc](#phpdoc)
    - [StyleCI](#styleci)
- [行为准则](#行为准则)

<a name="错误报告"></a>
## 错误报告

为了鼓励积极协作，Laravel 强烈鼓励提交拉取请求，而不仅仅是错误报告。只有标记为"准备审查"(而不是"草稿"状态)且新功能的所有测试都通过的拉取请求才会被审查。留在"草稿"状态的滞留非活跃拉取请求将在几天后被关闭。

但是，如果您提交错误报告，您的问题应该包含标题和清晰的问题描述。您还应包含尽可能多的相关信息以及演示该问题的代码示例。错误报告的目标是让您和其他人能够轻松复制该错误并开发修复方案。

请记住，创建错误报告是希望其他有同样问题的人能够与您合作解决它。不要期望错误报告会自动有任何活动或他人会立即修复它。创建错误报告是为了帮助您和其他人开始解决问题的道路。如果您想参与其中，可以通过修复[我们问题跟踪器中列出的任何错误](https://github.com/issues?q=is%3Aopen+is%3Aissue+label%3Abug+user%3Alaravel)来提供帮助。您必须通过 GitHub 认证才能查看所有 Laravel 问题。

如果您在使用 Laravel 时注意到不正确的 DocBlock、PHPStan 或 IDE 警告，请不要创建 GitHub 问题。请提交拉取请求来修复问题。

Laravel 源代码在 GitHub 上管理，每个 Laravel 项目都有对应的仓库：

<div class="content-list" markdown="1">

- [Laravel 应用](https://github.com/laravel/laravel)
- [Laravel Art](https://github.com/laravel/art)
- [Laravel Boost](https://github.com/laravel/boost)
- [Laravel 文档](https://github.com/laravel/docs)
- [Laravel Dusk](https://github.com/laravel/dusk)
- [Laravel Cashier Stripe](https://github.com/laravel/cashier)
- [Laravel Cashier Paddle](https://github.com/laravel/cashier-paddle)
- [Laravel Echo](https://github.com/laravel/echo)
- [Laravel Envoy](https://github.com/laravel/envoy)
- [Laravel Folio](https://github.com/laravel/folio)
- [Laravel 框架](https://github.com/laravel/framework)
- [Laravel Homestead](https://github.com/laravel/homestead) ([构建脚本](https://github.com/laravel/settler))
- [Laravel Horizon](https://github.com/laravel/horizon)
- [Laravel Passport](https://github.com/laravel/passport)
- [Laravel Pennant](https://github.com/laravel/pennant)
- [Laravel Pint](https://github.com/laravel/pint)
- [Laravel Prompts](https://github.com/laravel/prompts)
- [Laravel Reverb](https://github.com/laravel/reverb)
- [Laravel Sail](https://github.com/laravel/sail)
- [Laravel Sanctum](https://github.com/laravel/sanctum)
- [Laravel Scout](https://github.com/laravel/scout)
- [Laravel Socialite](https://github.com/laravel/socialite)
- [Laravel Telescope](https://github.com/laravel/telescope)
- [Laravel Livewire 入门套件](https://github.com/laravel/livewire-starter-kit)
- [Laravel React 入门套件](https://github.com/laravel/react-starter-kit)
- [Laravel Vue 入门套件](https://github.com/laravel/vue-starter-kit)

</div>

<a name="支持问题"></a>
## 支持问题

Laravel 的 GitHub 问题跟踪器不是用来提供 Laravel 帮助或支持的。请使用以下渠道之一：

<div class="content-list" markdown="1">

- [GitHub 讨论区](https://github.com/laravel/framework/discussions)
- [Laracasts 论坛](https://laracasts.com/discuss)
- [Laravel.io 论坛](https://laravel.io/forum)
- [StackOverflow](https://stackoverflow.com/questions/tagged/laravel)
- [Discord](https://discord.gg/laravel)
- [Larachat](https://larachat.co)
- [IRC](https://web.libera.chat/?nick=artisan&channels=#laravel)

</div>

<a name="核心开发讨论"></a>
## 核心开发讨论

您可以在 Laravel 框架仓库的 [GitHub 讨论板](https://github.com/laravel/framework/discussions)上提出新功能或改进现有 Laravel 行为的建议。如果您提议一个新功能，请愿意实现完成该功能所需的部分代码。

关于错误、新功能和现有功能实现的非正式讨论发生在 [Laravel Discord 服务器](https://discord.gg/laravel)的 `#internals` 频道。Laravel 维护者 Taylor Otwell 通常在工作日 UTC-06:00(或美国/芝加哥)上午 8 点到下午 5 点出现在频道中，其他时间也会不定期出现。

<a name="选择分支"></a>
## 选择分支

**所有**错误修复都应该发送到支持错误修复的最新版本(目前是 `12.x`)。错误修复应该**永远不要**发送到 `master` 分支，除非它们修复了仅存在于即将到来的发布版本中的功能。

与当前发布版本**完全向后兼容**的**次要**功能可以发送到最新的稳定分支(目前是 `12.x`)。

**主要**新功能或有破坏性变更的功能应始终发送到包含即将到来发布版本的 `master` 分支。

<a name="编译资源"></a>
## 编译资源

如果您提交的更改会影响编译文件，比如 `laravel/laravel` 仓库中的 `resources/css` 或 `resources/js` 中的大部分文件，请不要提交编译后的文件。由于它们的体积很大，维护者实际上无法审阅它们。这可能被利用作为向 Laravel 注入恶意代码的方式。为了防御性地防止这种情况，所有编译文件都将由 Laravel 维护者生成和提交。

<a name="安全漏洞"></a>
## 安全漏洞

如果您发现 Laravel 中的安全漏洞，请发送邮件至 Taylor Otwell 的邮箱 <a href="mailto:taylor@laravel.com">taylor@laravel.com</a>。所有安全漏洞都将得到及时处理。

<a name="编码风格"></a>
## 编码风格

Laravel 遵循 [PSR-2](https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-2-coding-style-guide.md) 编码标准和 [PSR-4](https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-4-autoloader.md) 自动加载标准。

<a name="phpdoc"></a>
### PHPDoc

以下是有效的 Laravel 文档块示例。请注意，`@param` 属性后面跟两个空格、参数类型、再两个空格，最后是变量名：

```php
/**
 * 向容器注册绑定。
 *
 * @param  string|array  $abstract
 * @param  \Closure|string|null  $concrete
 * @param  bool  $shared
 * @return void
 *
 * @throws \Exception
 */
public function bind($abstract, $concrete = null, $shared = false)
{
    // ...
}
```

当由于使用原生类型使得 `@param` 或 `@return` 属性冗余时，可以移除它们：

```php
/**
 * 执行任务。
 */
public function handle(AudioProcessor $processor): void
{
    // ...
}
```

但是，当原生类型是泛型时，请通过使用 `@param` 或 `@return` 属性指定泛型类型：

```php
/**
 * 获取消息的附件。
 *
 * @return array<int, \Illuminate\Mail\Mailables\Attachment>
 */
public function attachments(): array
{
    return [
        Attachment::fromStorage('/path/to/file'),
    ];
}
```

<a name="styleci"></a>
### StyleCI

不用担心您的代码样式不完美！[StyleCI](https://styleci.io/) 将在拉取请求合并后自动将任何样式修复合并到 Laravel 仓库中。这让我们能够专注于贡献的内容而不是代码样式。

<a name="行为准则"></a>
## 行为准则

Laravel 行为准则源自 Ruby 行为准则。任何违反行为准则的行为都可以报告给 Taylor Otwell(taylor@laravel.com)：

<div class="content-list" markdown="1">

- 参与者应对不同观点保持宽容。
- 参与者必须确保他们的语言和行为没有人身攻击和贬低他人的言论。
- 在解释他人的言行时，参与者应始终假设其出于善意。
- 任何合理认为是骚扰的行为都将不被容忍。

</div>