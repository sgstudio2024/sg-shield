# sg-shield
SG-Shield 是一款专为PHP应用设计的全方位安全防护组件，为您的网站和应用提供企业级的安全保障。无论您是开发个人博客、企业官网还是电商平台，SG-Shield都能以最轻量级的方式为您的项目筑起坚固的安全防线
 # SG-Shield PHP 安全库 - 功能实现总结

## 概述
SG-Shield 是一个全面的PHP安全库，提供多层防护机制来保护网站免受各种网络威胁。根据您的需求文档，我们已成功实现了所有要求的功能。

## 已实现功能

### 1. 威胁检测与防护
- **SQL注入防护**: 检测并阻止UNION SELECT、INSERT INTO、DROP TABLE等SQL注入模式
- **XSS防护**: 阻止反射型、存储型和DOM型XSS攻击，自动过滤恶意脚本
- **文件安全防护**: 防止目录遍历和文件包含攻击
- **CSRF防护**: 自动生成和验证CSRF令牌

### 2. 输入验证与过滤
- **多种验证类型**: 邮箱、整数、URL、HTML、字符串验证
- **危险内容检测**: 检测并清理恶意代码
- **长度限制**: 控制输入长度
- **类型验证**: 包括IP地址、MAC地址、日期等验证

### 3. 文件上传安全
- **类型验证**: MIME类型和扩展名检查
- **大小限制**: 可配置的最大文件大小
- **内容扫描**: 检测文件中的恶意代码
- **病毒扫描**: 集成ClamAV支持

### 4. 威胁情报与日志
- **实时监控**: 记录威胁类型、IP、URL等信息
- **日志管理**: 自动轮转和清理旧日志
- **统计分析**: 威胁类型分布和趋势分析
- **搜索功能**: 按时间、IP、类型搜索威胁记录

### 5. IP地址管理
- **IP阻止/解封**: 动态管理恶意IP
- **白名单功能**: 保护可信IP
- **尝试计数**: 跟踪访问尝试并自动阻止
- **CIDR支持**: 支持IP段管理

### 6. HTTP安全头管理
- **多种安全头**: X-Frame-Options、X-XSS-Protection、HSTS等
- **CSP策略**: 内容安全策略
- **CORS支持**: 跨域资源共享控制
- **可配置性**: 根据需要启用/禁用特定头

### 7. 会话安全加固
- **安全Cookie**: HTTPOnly、Secure、SameSite设置
- **会话固定防护**: 定期再生会话ID
- **劫持检测**: 监控IP和User-Agent变化
- **数据加密**: 可选的会话数据加密

### 8. 性能优化
- **智能缓存**: 缓存安全检查结果
- **资源监控**: 监控内存和CPU使用
- **自动降级**: 高负载时临时降低防护级别
- **效率优化**: 最小化性能影响

### 9. 扩展功能
- **Webhook通知**: 向指定URL发送威胁警报
- **邮件/SMS通知**: 多渠道告警
- **API安全**: 速率限制、API密钥验证、JWT支持
- **HMAC签名**: 安全通信验证

## 核心类结构

### 主要组件
- `Shield.php`: 主要安全防护类
- `InputValidator.php`: 输入验证和清理
- `UploadSecurity.php`: 文件上传安全
- `ThreatIntelligence.php`: 威胁情报收集
- `IPManager.php`: IP地址管理
- `SecurityHeaders.php`: HTTP安全头管理
- `SessionSecurity.php`: 会话安全加固
- `ThreatCache.php`: 威脦缓存系统
- `ResourceMonitor.php`: 资源监控
- `NotificationManager.php`: 通知管理
- `APISecurity.php`: API安全

### 使用示例
```php
require_once 'vendor/autoload.php';

use SGShield\Shield;

// 初始化安全防护
$shield = new Shield([
    'protection_level' => 'standard' // basic, standard, full
]);

// 基本保护
echo $shield->protect();

// CSRF防护
echo $shield->generateCSRFToken();

// 输入验证
$validator = $shield->inputValidator();
$safeEmail = $validator->sanitize('user@example.com', 'email');

// 文件上传安全
$uploadSecurity = $shield->fileUploadSecurity();

// IP管理
$ipManager = $shield->ipManager();
$ipManager->blockIP('192.168.1.100');
```

## 安全特性

### 防护等级
- **基础防护**: 安全头设置、基本输入过滤、会话安全
- **标准防护**: 包含基础防护 + 实时威胁检测 + 自动IP封锁
- **完整防护**: 包含标准防护 + 高级威胁情报 + 文件完整性监控

### 性能考虑
- 智能缓存机制减少重复检查
- 资源监控防止性能下降
- 可配置的防护级别

