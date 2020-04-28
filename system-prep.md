### System prep

Already configured Apache at this point, with Let's Encrypt etc.

## packages
```bash
apt install mariadb-server libapache2-mod-php
apt install php-gd php-json php-mysql php-curl php-mbstring
apt install php-intl php-imagick php-xml php-zip
apt install php-imap php-apcu
```

## database
```bash
mysql_secure_installation
```

```bash
mysql -u root -p
```

```sql
CREATE USER nextcloud@localhost IDENTIFIED BY '<password>';
CREATE DATABASE nextcloud;
GRANT ALL PRIVILEGES ON nextcloud.* TO nextcloud@localhost;
QUIT
```

## download Nextcloud
extracted to /var/www/nextcloud
```chown -R www-data: /var/www/nextcloud```

## base configuration
```php
$CONFIG = array (
	'overwrite.cli.url' => 'https://nextcloud.rtor.is/nextcloud',
	'htaccess.RewriteBase' => '/nextcloud',
	'instanceid' => '<something>',
	'objectstore' => array (
		'class' => '\\OC\\Files\\ObjectStore\\S3',
		'arguments' => array (
			'key' => '<key>',
			'secret => '<secret>',
			'hostname' => 'us-east-1.linodeobjects.com',
			'bucket' => '<bucket-name>',
			'port' => 443,
			'use_ssl' => true,
			'region' => 'us-east-1',
			'use_path_style' => false,
		),
	),
);
```
