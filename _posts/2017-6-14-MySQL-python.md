---
layout: post
title: MySQL-pythonを使ってみた
category: Development
comments: true
tag:
 - raspberrypi
 - MySQL
 - python
---

研究室の在室チェックに使うシステムを製作する過程でMySQLを使うんじゃねってなったので今回"MySQL-python"をお試しで使ってみました．

適当にソースコードを書きました．

```
# -*- coding: utf-8 -*-

import MySQLdb

# DBログイン
connection = MySQLdb.connect(host="localhost", db="RoomChecker", user="root", passwd="room", charset="utf8")
cursor = connection.cursor()

# SQL
# idmからユーザーの検索をする
idm = "xxxxxxx"
cursor.execute('select * from UserData where UserData_id = "'+ idm + '"')
result = cursor.fetchall()

# 表示
for row in result:
	print "----- Hit -----"
	print "UserData_id -------- " + row[0].encode('utf-8')
	print "UssrData_Name ------ " + row[1].encode('utf-8')
	if row[2] == 1:
		print "UserData_presence -- true"
	else:
		print "UserData_presence -- false"


# update文の使い方はここ
# >UPDATE "テーブル名" set "変更するカラム名" = "変更する値" where "変更するのを検索するカラム名" = "中身"

try:
#	cursor.execute('update UserData set UserData_presence = 1 where UserData_id = "yyyyyyy"')
	cursor.execute('select * from UserData')
	result = cursor.fetchall()
#	connection.commit()
except Exception as e:
	connection.rollback()
	raise e
finally:
	# 出力
	for row in result:
		print "----- Hit -----"
		print "UserData_id -------- " + row[0].encode('utf-8')
		print "UserData_name ------ " + row[1].encode('utf-8')
		if row[2] == 1:
			print "UserData_presence -- true"
		else:
			print "UserData_presence -- false"

	cursor.close()
	connection.close()
```
