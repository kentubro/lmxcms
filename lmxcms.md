First find the route according to the URL path ?m=Book&a=index. Enter c/index/BookAction.class.php in the root directory and view the index method:

![image.png](https://cdn.nlark.com/yuque/0/2024/png/25983428/1706883555805-75d5fdd2-d063-4347-86eb-b02d7cf538e4.png)

Enter the add function directly:  

![img](https://cdn.nlark.com/yuque/0/2024/png/25983428/1706884783355-a9a345ab-b609-45f3-96da-8ff3c5281653.png)

Follow up the addModel function:

![img](https://cdn.nlark.com/yuque/0/2024/png/25983428/1706884797289-4c09f25f-503b-4991-98ea-a1e792e62a0d.png)

Follow up with addDB

![img](https://cdn.nlark.com/yuque/0/2024/png/25983428/1706884830681-8ae4a679-335c-4166-96b2-d471ffdf81cb.png)

The problem comes here. The foreach loop is used to traverse the $data array. In each iteration, assign the key of the current element to $key and the value of the current element to $v. Although it attempts to surround the value with single quotes, this approach is not safe enough

![img](https://cdn.nlark.com/yuque/0/2024/png/25983428/1706884912674-871fce38-e82e-473e-93b5-c0aeff0a76a2.png)

Capture the data packet and add it to the value of mail)

![image.png](https://cdn.nlark.com/yuque/0/2024/png/25983428/1706885812666-56af3117-8769-4bf4-b807-ac6b2f10616b.png?x-oss-process=image%2Fresize%2Cw_937%2Climit_0)

Successful error reporting. By viewing the database information, we construct the following database statement

![image.png](https://cdn.nlark.com/yuque/0/2024/png/25983428/1706885869365-01e2a94e-edcb-4485-af19-085cb98decad.png)

Poc is as follows:

name=x&mail=x&tel=x&content=x&setbook=%E6%8F%90%E4%BA%A4&time&ischeck)values(user(),1,1,1,1,1,1)#=1

![image.png](https://cdn.nlark.com/yuque/0/2024/png/25983428/1706885967037-18ddd7e9-a348-476c-8bc9-e63a3bcf9841.png?x-oss-process=image%2Fresize%2Cw_937%2Climit_0)

Analyze why time&ischeck is used), because when writing the sql statement at the end, the data array is traversed. We write time into the data array when passing parameters in post, and the code itself adds time to the data array after post. Therefore, the time we pass in is earlier than the code itself. You can ignore the time of the code itself and implement our SQL injection. Here is a demonstration of revealing the user name.

![image.png](https://cdn.nlark.com/yuque/0/2024/png/25983428/1706886108765-d8a4820f-55c5-4818-a41f-31818fc41767.png) 

