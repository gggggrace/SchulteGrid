<template>
    <div class="hello">
        <!--Schulte Grid-->
        <h3 class="schulteTitle">Schulte Grid</h3>
        <div class="schulteHeader">
            <div class="schulteTime">
                <div>Time</div>
                <div>
                    <span class="schulteSeconds">{{seconds}}</span>
                </div>
            </div>
            <div class="schulteStage">
                <div>Stage</div>
                <div>1</div>
            </div>
            <div class="schulteBtn" :class="{conBtn:restart=='continue'}" @click="restartBtn()">{{restart}}</div>
        </div>
        <div class="schulteContent">
            <div class="schulteCell" v-for="(value,index) in cells"
                 :class="{correct:value.color =='correct', wrong:value.color =='wrong'}"
                 @click="cellClick(value.num,index)">{{value.num}}
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        name: 'hello',
        data () {
            return {
//      Schulte Grid
                cells: [
                    {num: 1, color: ''},
                    {num: 2, color: ''},
                    {num: 3, color: ''},
                    {num: 4, color: ''},
                    {num: 5, color: ''},
                    {num: 6, color: ''},
                    {num: 7, color: ''},
                    {num: 8, color: ''},
                    {num: 9, color: ''},
                    {num: 10, color: ''},
                    {num: 11, color: ''},
                    {num: 12, color: ''},
                    {num: 13, color: ''},
                    {num: 14, color: ''},
                    {num: 15, color: ''},
                    {num: 16, color: ''}
                ],

                order: 0,//记录点击顺序
                n: 0,//点击正确
                m: 0,//点击错误
                restart: "Restart",
                seconds: "00:00",
                time: "",
                dur:"0",

            }
        },
        methods: {
            alert2: function (m) {
                alert(this.m)
            },
            create: function () {
                const plusOne = x => x + 1;
                const isEven = x => (x % 5 === 0);
                const has99 = x => x !== 99;
//      const sum = (x, y) => x + y;

                const makeRange = x => [...new Array(x).keys()];
                const max = 10;

                const sum100 = makeRange(max).map(i => plusOne(i)).reduce((prev, currItem) => prev * currItem, 1);
                console.log(sum100);

                this.items.push(this.newItem);
                this.newItem = {
                    name: '',
                    age: 0,
                    sex: 'male'
                }
            },
            deleteItem: function (index) {
                this.items.splice(index, 1)
            },

            //数字随机排列
            randomSort(){
                let self = this;
                self.order = 0;
                let arr = self.cells;
                let res = [];
                for (let i = 0, len = arr.length; i < len; i++) {
                    let j = Math.floor(Math.random() * arr.length);
                    res[i] = arr[j];
                    arr.splice(j, 1);
                }
                self.cells = res;
            },
            //计时器
            timeCount(){
                let self = this;
                clearInterval(self.time);
                self.time = setInterval(function () {
                    self.dur = parseInt(self.dur) + 1;
                    let mm = Math.floor(self.dur / 60);
                    if(mm > 60) {

                    }
                    let ss = self.dur % 60;
                    self.seconds = self.addNum(mm) + ":" + self.addNum(ss);
                }, 1000)
            },
            //时间自动补全
            addNum(num){
                num = num < 10 ? ("0"+num) : num;
                return num;
            },
            //点击事件
            cellClick(num, index){
                let self = this;
                self.order++;
                if (self.order === num) {
                    self.cells[index].color = 'correct';
                    //清除定时器
                    if (self.order === 16) {
                        clearInterval(self.sec);
                        clearInterval(self.min);
                        self.restart = "continue"
                    }
                } else {
                    self.order--;
                    self.cells[index].color = 'wrong';
                }
                setTimeout(function () {
                    self.cells[index].color = '';
                }, 1000);
            },
            //重启
            restartBtn(){
                let self = this;
                self.randomSort();
                self.timeCount();
                self.restart = "Restart"
            },
        },
        mounted(){
            let self = this;
            self.randomSort();
            self.timeCount();
            self.restart = "Restart";
        }
    }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
    h1, h2 {
        font-weight: normal;
    }

    ul {
        list-style-type: none;
        padding: 0;
    }

    li {
        display: inline-block;
        margin: 0 10px;
    }

    a {
        color: #42b983;
    }

    .vFor {
        display: inline-block;
        margin-right: 10px
    }

    .fl {
        float: left
    }

    thead td {
        background-color: #42b983
    }

    td {
        border: 1px solid #eee;
        padding: 5px
    }

    /*.h30{height: 30px}*/

    body {
        font-size: 0.5rem;
    }

    .schulteTitle {
        text-align: center;
        margin: 10px;
    }

    .schulteHeader, .schulteContent {
        width: 310px;
        margin: 10px auto;
    }

    .schulteTime, .schulteStage, .schulteBtn {
        float: left;
        width: 70px;
        height: 70px;
        background-color: #fff;
        margin: 15px;
        text-align: center;
        line-height: 33px;
        border-radius: 5px;
        border: 1px solid #ededed;
    }

    .schulteBtn {
        line-height: 68px;
        cursor: pointer;
    }

    .schulteCell {
        width: 55px;
        height: 55px;
        margin: 10px;
        border-radius: 5px;
        border: 1px solid #ededed;
        float: left;
        background: #fff;
        text-align: center;
        line-height: 53px;
        transition: background 0.3s ease-out;
    }

    .correct {
        background: #5DADE2;
        color: #fff;
    }

    .wrong {
        background: #EC7063;
        color: #fff;
    }

    .conBtn {
        color: #EC7063;
    }
</style>
