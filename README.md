# MIS

/*
Navicat MySQL Data Transfer

Source Server         : localhost_3306
Source Server Version : 50712
Source Host           : localhost:3306
Source Database       : 电气设备保养单

Target Server Type    : MYSQL
Target Server Version : 50712
File Encoding         : 65001

Date: 2016-10-09 23:20:40
*/

SET FOREIGN_KEY_CHECKS=0;

-- ----------------------------
-- Table structure for `保养单maintenance`
-- ----------------------------
DROP TABLE IF EXISTS `保养单maintenance`;
CREATE TABLE `保养单maintenance` (
  `保养单ID` int(11) NOT NULL,
  `保养周期Period` varchar(45) DEFAULT NULL,
  `保养日期Date` date DEFAULT NULL,
  `保养员ID` int(11) NOT NULL,
  PRIMARY KEY (`保养单ID`),
  CONSTRAINT `保养员ID` FOREIGN KEY (`保养单ID`) REFERENCES `保养员person` (`保养员ID`) ON DELETE NO ACTION ON UPDATE NO ACTION
) ENGINE=InnoDB DEFAULT CHARSET=utf8;

-- ----------------------------
-- Records of 保养单maintenance
-- ----------------------------
INSERT INTO `保养单maintenance` VALUES ('1', '年检', '2014-10-15', '1');
INSERT INTO `保养单maintenance` VALUES ('2', '年检', '2014-11-11', '2');

-- ----------------------------
-- Table structure for `保养员person`
-- ----------------------------
DROP TABLE IF EXISTS `保养员person`;
CREATE TABLE `保养员person` (
  `保养员ID` int(11) NOT NULL,
  `保养员姓名Name` varchar(45) DEFAULT NULL,
  PRIMARY KEY (`保养员ID`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8;

-- ----------------------------
-- Records of 保养员person
-- ----------------------------
INSERT INTO `保养员person` VALUES ('1', '王二');
INSERT INTO `保养员person` VALUES ('2', '张三');
INSERT INTO `保养员person` VALUES ('3', '李四');
INSERT INTO `保养员person` VALUES ('4', '宋低昂');

-- ----------------------------
-- Table structure for `保养消耗`
-- ----------------------------
DROP TABLE IF EXISTS `保养消耗`;
CREATE TABLE `保养消耗` (
  `保养消耗ID` int(11) NOT NULL,
  `材料名称` varchar(45) DEFAULT NULL,
  `材料数量` int(11) DEFAULT NULL,
  PRIMARY KEY (`保养消耗ID`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8;

-- ----------------------------
-- Records of 保养消耗
-- ----------------------------
INSERT INTO `保养消耗` VALUES ('111', '瓷瓶', '5');

-- ----------------------------
-- Table structure for `保养记录record`
-- ----------------------------
DROP TABLE IF EXISTS `保养记录record`;
CREATE TABLE `保养记录record` (
  `保养记录ID` int(11) NOT NULL,
  `保养单ID` int(11) NOT NULL,
  `设备ID` int(11) NOT NULL,
  `完成情况` varchar(100) DEFAULT NULL,
  `备注` varchar(100) DEFAULT NULL,
  PRIMARY KEY (`保养记录ID`),
  KEY `保养单ID_idx` (`保养单ID`),
  KEY `设备ID_idx` (`设备ID`),
  CONSTRAINT `保养单ID` FOREIGN KEY (`保养单ID`) REFERENCES `保养单maintenance` (`保养单ID`) ON DELETE NO ACTION ON UPDATE NO ACTION,
  CONSTRAINT `设备ID` FOREIGN KEY (`设备ID`) REFERENCES `设备单equipment` (`设备ID`) ON DELETE NO ACTION ON UPDATE NO ACTION
) ENGINE=InnoDB DEFAULT CHARSET=utf8;

-- ----------------------------
-- Records of 保养记录record
-- ----------------------------
INSERT INTO `保养记录record` VALUES ('1', '1', '1', '已完成', null);

-- ----------------------------
-- Table structure for `保养项目project`
-- ----------------------------
DROP TABLE IF EXISTS `保养项目project`;
CREATE TABLE `保养项目project` (
  `项目ID` int(11) NOT NULL,
  `保养内容Content` varchar(100) DEFAULT NULL,
  `设备ID` int(11) NOT NULL,
  PRIMARY KEY (`项目ID`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8;

-- ----------------------------
-- Records of 保养项目project
-- ----------------------------
INSERT INTO `保养项目project` VALUES ('1', '检查6000V接线盒内瓷瓶、端子', '1');
INSERT INTO `保养项目project` VALUES ('2', '接线盒内卫生清洁', '1');
INSERT INTO `保养项目project` VALUES ('3', '检查电缆引线、穿线管、接地线', '1');
INSERT INTO `保养项目project` VALUES ('4', '检查进线口密封情况', '1');
INSERT INTO `保养项目project` VALUES ('5', '检查前后轴承温度传感器的接线盒', '1');
INSERT INTO `保养项目project` VALUES ('6', '检查定子绕组温度传感器的接线盒', '1');
INSERT INTO `保养项目project` VALUES ('7', '检查防潮加热器的接线盒', '1');

-- ----------------------------
-- Table structure for `设备单equipment`
-- ----------------------------
DROP TABLE IF EXISTS `设备单equipment`;
CREATE TABLE `设备单equipment` (
  `设备ID` int(11) NOT NULL,
  `设备名称Name` varchar(45) NOT NULL,
  `设备类型ID` int(11) DEFAULT NULL,
  `最后保养时间Date` date DEFAULT NULL,
  PRIMARY KEY (`设备ID`),
  KEY `设备类型Type_idx` (`设备类型ID`),
  CONSTRAINT `设备类型ID` FOREIGN KEY (`设备类型ID`) REFERENCES `设备类型表type` (`设备类型ID`) ON DELETE NO ACTION ON UPDATE NO ACTION
) ENGINE=InnoDB DEFAULT CHARSET=utf8;

-- ----------------------------
-- Records of 设备单equipment
-- ----------------------------
INSERT INTO `设备单equipment` VALUES ('1', '6000V及以上电机', '11', '2016-10-01');
INSERT INTO `设备单equipment` VALUES ('2', '6000V以下不带振动电机', '22', '2015-10-08');

-- ----------------------------
-- Table structure for `设备类型表type`
-- ----------------------------
DROP TABLE IF EXISTS `设备类型表type`;
CREATE TABLE `设备类型表type` (
  `设备类型ID` int(11) NOT NULL,
  `设备类型Type` varchar(45) DEFAULT NULL,
  PRIMARY KEY (`设备类型ID`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8;

-- ----------------------------
-- Records of 设备类型表type
-- ----------------------------
INSERT INTO `设备类型表type` VALUES ('11', '电机');
INSERT INTO `设备类型表type` VALUES ('22', '采样机');


查询
1、	查询设备保养信息

![](/截图1.png)
![](/截图2.png)
![](/截图3.png)
2、查询到期设备
![](/截图4.png)

ER图
![](/截图6.png)
