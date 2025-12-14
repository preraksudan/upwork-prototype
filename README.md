CREATE TABLE `admin_users` (
  `id` int NOT NULL AUTO_INCREMENT,
  `username` varchar(50) COLLATE utf8mb4_general_ci NOT NULL,
  `password` varchar(255) COLLATE utf8mb4_general_ci NOT NULL,
  PRIMARY KEY (`id`),
  UNIQUE KEY `username` (`username`)
);

CREATE TABLE `spanish_audio` (
  `id` int(10) unsigned NOT NULL,
  `audio_file` varchar(255) NOT NULL,
  `created` timestamp NOT NULL DEFAULT current_timestamp(),
  `updated` timestamp NOT NULL DEFAULT current_timestamp() ON UPDATE current_timestamp(),
  PRIMARY KEY (`id`,`audio_file`),
  KEY `idx_audio` (`id`),
  CONSTRAINT `spanish_audio_ibfk_1` FOREIGN KEY (`id`) REFERENCES `spanish_to_english` (`id`) ON DELETE CASCADE ON UPDATE CASCADE
);

CREATE TABLE `spanish_pos` (
  `id` int(10) unsigned NOT NULL,
  `pos` varchar(64) NOT NULL,
  `created` timestamp NOT NULL DEFAULT current_timestamp(),
  `updated` timestamp NOT NULL DEFAULT current_timestamp() ON UPDATE current_timestamp(),
  PRIMARY KEY (`id`,`pos`),
  KEY `pos` (`pos`),
  KEY `idx_pos` (`id`),
  CONSTRAINT `spanish_pos_ibfk_1` FOREIGN KEY (`id`) REFERENCES `spanish_to_english` (`id`) ON DELETE CASCADE ON UPDATE CASCADE,
  CONSTRAINT `spanish_pos_ibfk_2` FOREIGN KEY (`pos`) REFERENCES `pos_definitions` (`pos`) ON DELETE CASCADE ON UPDATE CASCADE
);

CREATE TABLE `spanish_to_english` (
  `id` int(10) unsigned NOT NULL AUTO_INCREMENT,
  `spanish` varchar(255) NOT NULL,
  `english` varchar(255) NOT NULL,
  `flag` tinyint(1) DEFAULT NULL,
  `created` timestamp NOT NULL DEFAULT current_timestamp(),
  `updated` timestamp NOT NULL DEFAULT current_timestamp() ON UPDATE current_timestamp(),
  PRIMARY KEY (`id`),
  KEY `idx_spanish` (`spanish`),
  KEY `idx_english` (`english`)
);


CREATE TABLE `pos_definitions` (
  `pos` varchar(64) NOT NULL,
  `description` varchar(128) NOT NULL,
  `created` timestamp NOT NULL DEFAULT current_timestamp(),
  `updated` timestamp NOT NULL DEFAULT current_timestamp() ON UPDATE current_timestamp(),
  PRIMARY KEY (`pos`)
);

<img width="472" height="289" alt="Screenshot 2025-12-14 at 3 23 41 PM" src="https://github.com/user-attachments/assets/274c9560-94b7-4e64-ac18-50440c3c97cf" />

<img width="540" height="403" alt="Screenshot 2025-12-14 at 3 23 25 PM" src="https://github.com/user-attachments/assets/84274a86-7bfd-4d9a-88ed-1d131872f480" />



