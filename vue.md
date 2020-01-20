
Q：v-if和v-for哪个优先级高？如果两个同时出现，应该怎么优化得到更好的性能？

A： vue处理指令时，v-for 比 v-if 优先级更高,这意味着 v-if 将分别重复运行于每个 v-for 循环中。

   如果 v-if 和 v-for 只能放在同一级标签中，使用计算属性进行改造：
   (比如 v-for="user in users" v-if="user.isActive")。在这种情形下，请将 users替换为一个计算属性 (比如 activeUsers)，让其返回过滤后的列表。

    将：
    <ul>
    <li v-for="user in users" v-if="user.isActive" :key="user.id">
        {{ user.name }}
    </li>
    </ul>


    换成：

    <ul>
    <li v-for="user in activeUsers" :key="user.id">
        {{ user.name }}
    </li>
    </ul>
    computed: {
        activeUsers: function () {
            return this.users.filter(function (user) {
            return user.isActive
            })
        }
    }
