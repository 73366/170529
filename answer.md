Установить mongodb.
======= done

Скачать файл results.json.

Выполнить команду:

mongoimport --db yourDbName --collection yourCollectionName --file ~/results.json --jsonArray, где:

~/results.json - Ваш путь к файлу
yourDbName - имя Вашей базы данных
yourCollectionName - имя Вашей коллекции

mongoimport --db testDBhw290517 --collection testCollect --file d:/test/data/dataSample.json --jsonArray
======= done

Запустить консоль командой mongo. 
======= done

Выполнить команду use yourDbName.
======= done

use testDBhw290517

написать следующие запросы:

1) Написать запрос для поиска всех студентов, у которых score > 87% и < 93% по любому из типов выполненных заданий.

======= answer 

db.testCollect.find({scores:{$elemMatch:{$and:[{score:{$gt:87}},{score:{$lt:93}}]}}}).pretty()

======= result

> db.testCollect.find({scores:{$elemMatch:{$and:[{score:{$gt:87}},{score:{$lt:93}}]}}}).count()

52


2) Написать запрос-агрегацию для выборки всех студентов, у которых результат по экзамену (type: "exam") более 90% (использование unwind)

======= answer

db.testCollect.aggregate([{$unwind:"$scores"},{$match:{$and:[{"scores.type":"exam"},{"scores.score":{$gt:90}}]}}]).pretty()

======= result

> db.testCollect.aggregate([{$unwind:"$scores"},{$match:{$and:[{"scores.type":"exam"},{"scores.score":{$gt:90}}]}}]).pretty().itcount()

18


3) Студентам с именем Dusti Lemmond добавить поле “accepted” со значением true.

======= answer

db.testCollect.update({name:"Dusti Lemmond"},{$set:{accepted:true}}, {multi: true})

======= result

> db.testCollect.find({name:"Dusti Lemmond"}).pretty()

{
        "_id" : 60,
        "name" : "Dusti Lemmond",
        "scores" : [
                {
                        "type" : "exam",
                        "score" : 17.27725327681863
                },
                {
                        "type" : "quiz",
                        "score" : 83.24439414725833
                },
                {
                        "type" : "homework",
                        "score" : 81.84258722611811
                },
                {
                        "type" : "homework",
                        "score" : 24.70433764307496
                }
        ],
        "accepted" : true
}
{
        "_id" : 2001,
        "name" : "Dusti Lemmond",
        "scores" : [
                {
                        "type" : "exam",
                        "score" : 76.84555652243097
                },
                {
                        "type" : "quiz",
                        "score" : 28.028382208262382
                },
                {
                        "type" : "homework",
                        "score" : 62.46944003411778
                },
                {
                        "type" : "homework",
                        "score" : 78.73446824963553
                }
        ],
        "accepted" : true

		=============
