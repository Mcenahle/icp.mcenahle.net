# icp.mcenahle.net

继萌ICP备案之后，就一直想要搞一个自己的虚拟备案系统，终于在7月19日编写完第一版程序，于21日基本编写完成，于25日决定采用GPLv3开源许可证进行开源，于27日发布在Github上！

**注意：**

本项目使用附加条款的 [GPLv3 开源许可协议 ↗](https://www.gnu.org/licenses/gpl-3.0.zh-cn.html#license-text) 进行开源。违反者将被撤销此项目的使用权。

附加条款如下：（依据 GPLv3 开源协议第七条）

1. 当您分发该程序的修改版本时，您必须以一种合理的方式修改该程序的名称或版本号，以示其与原始版本不同（依据 GPLv3, 7(c)）；
2. 您不得移除该程序所显示的版权声明（依据 GPLv3, 7(b)）.

## 开始使用

在使用前，务必先完成数据库和表的搭建。执行SQL查询以完成搭建：

```SQL
CREATE DATABASE record_system;

USE record_system;

CREATE TABLE records (
    id INT AUTO_INCREMENT PRIMARY KEY,
    site_name VARCHAR(255) NOT NULL,
    email VARCHAR(255) NOT NULL,
    url VARCHAR(255) NOT NULL,
    site_description TEXT,
    status VARCHAR(50) DEFAULT 'pending',
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

CREATE TABLE admin_users (
    id INT AUTO_INCREMENT PRIMARY KEY,
    username VARCHAR(50) NOT NULL,
    password VARCHAR(255) NOT NULL
);
    INSERT INTO admin_users (username, password) VALUES ('admin', 'admin123');
		
CREATE TABLE reports (
    id INT AUTO_INCREMENT PRIMARY KEY,
    record_id INT NOT NULL,
    report_reason TEXT NOT NULL,
    status ENUM('pending', 'reviewed') DEFAULT 'pending',
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (record_id) REFERENCES records(id)
);
```

注意，上面的“admin”和“admin123”是后期登录管理后台的用户名和密码。

随后，将压缩包上传至网站根目录下，即可开始使用了！
