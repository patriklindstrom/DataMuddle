##About DataMuddler##
###User Story###
Christopher has data files in production environment that needs to be sent to test environment. They contain information that is sensitive and need to be changed so it can no longer be tracked to the original person. 

The files are connected. For example one file can contain name, account number that connects it with other data in other files.

Therr are huge data files. New datafiles appear everyday. The usage of this program might increase. So **performance is important**. The application must **scale** easily.

The following data muddling techniques would be nice to have:


- **Dictionary replace**. Change field that has same meaning and value in many files. Exemple: *A male person field; Forename should have it replaced with other male forename. A streetname should be replaced with other existing streetname, A social security number of personnumber chould be changed new value that is looked up in a dictonary*
- **Number muddling**. A transaction value could change by 1-2%. So a single transaction with unusual sum could not be backtraced. Example: * So if I buy an item for 98.98 i will not find in the muddled filed in the file because it is changed to 102.35 . The changed value must adhere to the [Benfords law](http://en.wikipedia.org/wiki/Benford%27s_law )
- **Transaction muddling** Adds random extra copies of transactions. This is so it is harder to find on single odd transaction and backtrack other muddling from that. Exmaple:*You know that you are the only one who bought one item 2012-02-29 and try to find this transaction in muddled data. So this muddling makes it harde because it might be two or more transactions - n number of transactions are faked.
- **Algoritm muddling** Function that transforms data to other unique value. Used for fields thar are not connected to other field. Example: *A Cars register number: "NYG 528" Could be replaced with "MGH 639"* 
- **Shuffle muddling** A field that has no connections to other files and has low variation per row could be shuffled. Example:*A green car will get the colour value from other car and become red car*

The dictionary must be encrypted if stored on disk.
 
Import of data and what muddlings should be used should be handled by configuration or script language so no coding is necceary to change muddling strategies or import/export of data.

###Solution Description###
(Work on this) Decide what fields in a file that needs.

###Technical implementation###



- Reddis key value store as dictonary
- Rhino-ETL as ETL framework. See this articla about hello world Rhino.[hello-world-rhino-etl/](http://www.lcube.se/hello-world-rhino-etl/)
- Encrypt saved Redis dictonary with public key. See this about Redis: [http://redis.io/](http://redis.io/) and Redis for windows: [Redis-on-Windows-Getting-Started](http://channel9.msdn.com/Blogs/Interoperability/Redis-on-Windows-Getting-Started)
- Encrypt script / config also? [gpg encryption](http://www.codeproject.com/Articles/457453/PGP-Encryption-with-Csharp)



