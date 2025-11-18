# 发布说明

- [版本控制方案](#版本控制方案)
- [支持政策](#支持政策)
- [Laravel 12](#laravel-12)

<a name="版本控制方案"></a>
## 版本控制方案

Laravel 及其其他第一方包遵循 [语义化版本控制](https://semver.org)。主要框架版本每年发布一次(~第一季度)，而次要和补丁版本可能每周发布一次。次要和补丁版本应该**永远不会**包含破坏性变更。

在您的应用程序或包中引用 Laravel 框架或其组件时，应始终使用如 `^12.0` 这样的版本约束，因为 Laravel 的主要版本确实包含破坏性变更。但是，我们努力确保您可以在一天或更短的时间内更新到新的主要版本。

<a name="命名参数"></a>
#### 命名参数

[命名参数](https://www.php.net/manual/en/functions.arguments.php#functions.named-arguments)不受 Laravel 向后兼容性指南的覆盖。我们可能会在必要时重命名函数参数以改进 Laravel 代码库。因此，在调用 Laravel 方法时使用命名参数应谨慎进行，并理解参数名称将来可能会改变。

<a name="支持政策"></a>
## 支持政策

对于所有 Laravel 发布版本，错误修复提供 18 个月，安全修复提供 2 年。对于所有附加库，只有最新的主要版本接收错误修复。此外，请查看 Laravel [支持的数据库版本](/docs/{{version}}/database/database#introduction)。

<div class="overflow-auto">

| 版本 | PHP (*)   | 发布日期           | 错误修复截止日期    | 安全修复截止日期   |
| ---- | --------- | ------------------ | ------------------- | ------------------ |
| 10   | 8.1 - 8.3 | 2023年2月14日      | 2024年8月6日        | 2025年2月4日       |
| 11   | 8.2 - 8.4 | 2024年3月12日      | 2025年9月3日        | 2026年3月12日      |
| 12   | 8.2 - 8.4 | 2025年2月24日      | 2026年8月13日       | 2027年2月24日      |
| 13   | 8.3 - 8.4 | 2026年第一季度     | 2027年第三季度      | 2028年第一季度     |

</div>

<div class="version-colors">
    <div class="end-of-life">
        <div class="color-box"></div>
        <div>生命周期结束</div>
    </div>
    <div class="security-fixes">
        <div class="color-box"></div>
        <div>仅安全修复</div>
    </div>
</div>

(*) 支持的 PHP 版本

<a name="laravel-12"></a>
## Laravel 12

Laravel 12 通过更新上游依赖项并引入新的 React、Vue 和 Livewire 入门套件(包括使用 [WorkOS AuthKit](https://authkit.com) 进行用户身份验证的选项)继续改进 Laravel 11.x。我们的入门套件的 WorkOS 变体提供了社交认证、通行密钥和单点登录支持。

<a name="最小破坏性变更"></a>
### 最小破坏性变更

在此发布周期间，我们的大部分关注点都是尽量减少破坏性变更。相反，我们致力于全年发布不会破坏现有应用程序的持续生活质量改进。

因此，Laravel 12 发布是一个相对较小的"维护发布"，以升级现有依赖项。鉴于此，大多数 Laravel 应用程序可以无需更改任何应用程序代码就升级到 Laravel 12。

<a name="新应用入门套件"></a>
### 新应用入门套件

Laravel 12 为 React、Vue 和 Livewire 引入了新的[应用入门套件](/docs/{{version}}/getting-started/starter-kits)。React 和 Vue 入门套件使用 Inertia 2、TypeScript、[shadcn/ui](https://ui.shadcn.com) 和 Tailwind，而 Livewire 入门套件使用基于 Tailwind 的 [Flux UI](https://fluxui.dev) 组件库和 Laravel Volt。

React、Vue 和 Livewire 入门套件都使用 Laravel 内置的身份验证系统，提供登录、注册、密码重置、邮箱验证等功能。此外，我们正在为每个入门套件引入 [WorkOS AuthKit 驱动](https://authkit.com)的变体，提供社交认证、通行密钥和单点登录支持。WorkOS 为每月活跃用户不超过 100 万的应用程序提供免费认证。

随着我们新应用入门套件的推出，Laravel Breeze 和 Laravel Jetstream 将不再接收额外更新。

要开始使用我们的新入门套件，请查看[入门套件文档](/docs/{{version}}/getting-started/starter-kits)。