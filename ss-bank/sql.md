---
description: BANK USERS ( Main Sql )
---

# SQL

```sql
CREATE TABLE IF NOT EXISTS `bank_users` (
  `id` int(11) NOT NULL AUTO_INCREMENT,
  `name` varchar(50) NOT NULL,
  `identifier` varchar(50) NOT NULL,
  `charidentifier` int(11) NOT NULL,
  `money` double(22,2) DEFAULT 0.00,
  `gold` double(22,2) DEFAULT 0.00,
  `time` int(11) DEFAULT 0,
  `loan` int(11) DEFAULT 0,
  `loantime` int(11) DEFAULT 0,
  `payback` int(11) DEFAULT 0,
  `firstname` varchar(50) DEFAULT NULL,
  `lastname` varchar(50) DEFAULT NULL,
  `freeze` int(11) NOT NULL DEFAULT 0,
  PRIMARY KEY (`id`),
  KEY `name` (`name`)
) ENGINE=InnoDB AUTO_INCREMENT=7421 DEFAULT CHARSET=latin1;
```

BANK CHECKS ( Only if you enable and use it )

```sql
CREATE TABLE IF NOT EXISTS `bank_checks` (
  `id` varchar(100) NOT NULL DEFAULT '0',
  `owner` varchar(500) DEFAULT NULL,
  `destinate` varchar(500) DEFAULT NULL,
  `date` varchar(50) DEFAULT NULL,
  `expire` varchar(50) DEFAULT NULL,
  `bank` varchar(50) DEFAULT NULL,
  `amount` int(11) DEFAULT NULL,
  `description` varchar(500) DEFAULT NULL,
  `timer` int(11) DEFAULT NULL,
  PRIMARY KEY (`id`)
) ENGINE=InnoDB DEFAULT CHARSET=latin1;
```

BANK HISTORY ( Only if you enable and use it )

```sql
CREATE TABLE IF NOT EXISTS `bank_history` (
  `id` int(11) NOT NULL AUTO_INCREMENT,
  `charid` int(11) DEFAULT NULL,
  `info` varchar(500) DEFAULT NULL,
  `type` varchar(50) DEFAULT NULL,
  `amount` decimal(20,6) DEFAULT NULL,
  `bank` varchar(50) DEFAULT NULL,
  `date` varchar(50) DEFAULT NULL,
  `timer` int(11) DEFAULT NULL,
  PRIMARY KEY (`id`)
) ENGINE=InnoDB AUTO_INCREMENT=22 DEFAULT CHARSET=latin1;
```

