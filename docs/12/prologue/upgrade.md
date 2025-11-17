# 升级指南

- [从 11.x 升级到 12.0](#upgrade-12.0)

<a name="高影响变更"></a>
## 高影响变更

<div class="content-list" markdown="1">

- [更新依赖项](#更新依赖项)
- [更新 Laravel 安装程序](#更新-laravel-安装程序)

</div>

<a name="中影响变更"></a>
## 中影响变更

<div class="content-list" markdown="1">

- [模型和 UUIDv7](#模型和-uuidv7)

</div>

<a name="低影响变更"></a>
## 低影响变更

<div class="content-list" markdown="1">

- [Carbon 3](#carbon-3)
- [并发结果索引映射](#并发结果索引映射)
- [容器类依赖解析](#容器类依赖解析)
- [图像验证现在排除 SVG](#图像验证)
- [本地文件系统磁盘默认根路径](#本地文件系统磁盘默认根路径)
- [多模式数据库检查](#多模式数据库检查)
- [嵌套数组请求合并](#嵌套数组请求合并)

</div>

<a name="upgrade-12.0"></a>
## 从 11.x 升级到 12.0

#### 预计升级时间：5 分钟

> [!NOTE]
> 我们尝试记录每一个可能的破坏性变更。由于这些破坏性变更中的一些位于框架的晦涩部分，只有一部分变更实际上会影响您的应用程序。想要节省时间吗？您可以使用 [Laravel Shift](https://laravelshift.com/) 来帮助自动化您的应用程序升级。

<a name="更新依赖项"></a>
### 更新依赖项

**影响可能性：高**

您应该在应用程序的 `composer.json` 文件中更新以下依赖项：

<div class="content-list" markdown="1">

- `laravel/framework` 更新到 `^12.0`
- `phpunit/phpunit` 更新到 `^11.0`
- `pestphp/pest` 更新到 `^3.0`

</div>

<a name="carbon-3"></a>
#### Carbon 3

**影响可能性：低**

对 [Carbon 2.x](https://carbon.nesbot.com/docs/) 的支持已被移除。所有 Laravel 12 应用程序现在都需要 [Carbon 3.x](https://carbon.nesbot.com/docs/#api-carbon-3)。

<a name="更新-laravel-安装程序"></a>
### 更新 Laravel 安装程序

如果您使用 Laravel 安装程序 CLI 工具创建新的 Laravel 应用程序，则应更新您的安装程序安装以与 Laravel 12.x 和[新的 Laravel 入门套件](https://laravel.com/starter-kits)兼容。如果您通过 `composer global require` 安装了 Laravel 安装程序，您可以使用 `composer global update` 更新安装程序：

```shell
composer global update laravel/installer
```

如果您最初通过 `php.new` 安装了 PHP 和 Laravel，您可以简单地重新运行适用于您操作系统的 `php.new` 安装命令来安装最新版本的 PHP 和 Laravel 安装程序：

```shell tab=macOS
/bin/bash -c "$(curl -fsSL https://php.new/install/mac/8.4)"
```

```shell tab=Windows PowerShell
# 以管理员身份运行...
Set-ExecutionPolicy Bypass -Scope Process -Force; [System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072; iex ((New-Object System.Net.WebClient).DownloadString('https://php.new/install/windows/8.4'))
```

```shell tab=Linux
/bin/bash -c "$(curl -fsSL https://php.new/install/linux/8.4)"
```

或者，如果您使用的是 [Laravel Herd](https://herd.laravel.com) 捆绑的 Laravel 安装程序副本，您应该将 Herd 安装更新到最新版本。

<a name="认证"></a>
### 认证

<a name="更新-databasetokenrepository-构造函数签名"></a>
#### 更新 `DatabaseTokenRepository` 构造函数签名

**影响可能性：极低**

`Illuminate\Auth\Passwords\DatabaseTokenRepository` 类的构造函数现在期望 `$expires` 参数以秒为单位，而不是分钟。

<a name="并发"></a>
### 并发

<a name="并发结果索引映射"></a>
#### 并发结果索引映射

**影响可能性：低**

当使用关联数组调用 `Concurrency::run` 方法时，并发操作的结果现在会返回与其关联的键：

```php
$result = Concurrency::run([
    'task-1' => fn () => 1 + 1,
    'task-2' => fn () => 2 + 2,
]);

// ['task-1' => 2, 'task-2' => 4]
```

<a name="容器"></a>
### 容器

<a name="容器类依赖解析"></a>
#### 容器类依赖解析

**影响可能性：低**

依赖注入容器现在在解析类实例时会考虑类属性的默认值。如果您之前依赖容器在没有默认值的情况下解析类实例，您可能需要调整应用程序以适应这种新行为：

```php
class Example
{
    public function __construct(public ?Carbon $date = null) {}
}

$example = resolve(Example::class);

// <= 11.x
$example->date instanceof Carbon;

// >= 12.x
$example->date === null;
```

<a name="数据库"></a>
### 数据库

<a name="多模式数据库检查"></a>
#### 多模式数据库检查

**影响可能性：低**

`Schema::getTables()`、`Schema::getViews()` 和 `Schema::getTypes()` 方法现在默认包含所有模式的结果。您可以传递 `schema` 参数仅检索给定模式的结果：

```php
// 所有模式上的所有表...
$tables = Schema::getTables();

// 'main' 模式上的所有表...
$tables = Schema::getTables(schema: 'main');

// 'main' 和 'blog' 模式上的所有表...
$tables = Schema::getTables(schema: ['main', 'blog']);
```

`Schema::getTableListing()` 方法现在默认返回模式限定的表名。您可以传递 `schemaQualified` 参数按需更改行为：

```php
$tables = Schema::getTableListing();
// ['main.migrations', 'main.users', 'blog.posts']

$tables = Schema::getTableListing(schema: 'main');
// ['main.migrations', 'main.users']

$tables = Schema::getTableListing(schema: 'main', schemaQualified: false);
// ['migrations', 'users']
```

`db:table` 和 `db:show` 命令现在在 MySQL、MariaDB 和 SQLite 上输出所有模式的结果，就像 PostgreSQL 和 SQL Server 一样。

<a name="更新-blueprint-构造函数签名"></a>
#### 更新 `Blueprint` 构造函数签名

**影响可能性：极低**

`Illuminate\Database\Schema\Blueprint` 类的构造函数现在期望其第一个参数是 `Illuminate\Database\Connection` 的实例。

<a name="eloquent"></a>
### Eloquent

<a name="模型和-uuidv7"></a>
#### 模型和 UUIDv7

**影响可能性：中等**

`HasUuids` trait 现在返回与 UUID 规范第 7 版兼容的 UUID(有序 UUID)。如果您想继续为模型 ID 使用有序 UUIDv4 字符串，现在应该使用 `HasVersion4Uuids` trait：

```php
use Illuminate\Database\Eloquent\Concerns\HasUuids; // [tl! remove]
use Illuminate\Database\Eloquent\Concerns\HasVersion4Uuids as HasUuids; // [tl! add]
```

`HasVersion7Uuids` trait 已被移除。如果您之前使用过此 trait，应改用 `HasUuids` trait，它现在提供相同的行为。

<a name="请求"></a>
### 请求

<a name="嵌套数组请求合并"></a>
#### 嵌套数组请求合并

**影响可能性：低**

`$request->mergeIfMissing()` 方法现在允许使用"点"符号合并嵌套数组数据。如果您之前依赖此方法创建包含"点"符号版本键的顶级数组键，您可能需要调整应用程序以适应这种新行为：

```php
$request->mergeIfMissing([
    'user.last_name' => 'Otwell',
]);
```

<a name="存储"></a>
### 存储

<a name="本地文件系统磁盘默认根路径"></a>
#### 本地文件系统磁盘默认根路径

**影响可能性：低**

如果您的应用程序未在文件系统配置中明确定义 `local` 磁盘，Laravel 现在将默认将本地磁盘的根目录设为 `storage/app/private`。在之前的版本中，这默认为 `storage/app`。因此，调用 `Storage::disk('local')` 将从 `storage/app/private` 读取和写入，除非另有配置。要恢复以前的行为，您可以手动定义 `local` 磁盘并设置所需的根路径。

<a name="验证"></a>
### 验证

<a name="图像验证"></a>
#### 图像验证现在排除 SVG

**影响可能性：低**

`image` 验证规则默认不再允许 SVG 图像。如果您想在使用 `image` 规则时允许 SVG，必须明确允许它们：

```php
use Illuminate\Validation\Rules\File;

'photo' => 'required|image:allow_svg'

// 或者...
'photo' => ['required', File::image(allowSvg: true)],
```

<a name="杂项"></a>
### 杂项

我们还鼓励您查看 `laravel/laravel` [GitHub 仓库](https://github.com/laravel/laravel)中的变更。虽然许多变更不是必需的，但您可能希望让这些文件与您的应用程序保持同步。这些变更中的一些将在此升级指南中介绍，但其他变更，如配置文件或注释的更改，将不会介绍。您可以使用 [GitHub 对比工具](https://github.com/laravel/laravel/compare/11.x...12.x)轻松查看变更，并选择哪些更新对您重要。