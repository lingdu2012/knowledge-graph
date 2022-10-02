<template>
  <div style="width: 100%;height:100%;">
    <button @click="updateData">添加节点</button>
    <div id="neo4jd3" ref="neo4jd3" style="position:relative;width: 100%;height:100%;"></div>
  </div>
</template>

<script>
  import myNeo4jd3 from "../../src/util/neo4jd3.js";
  /**
 * 图谱初始化数据结构
 * 本知识图谱支持两种数据结构
 */
 // 第一种,Neo4j数据结构，更新数据使用updateWithNeo4jData
let initJson={
   "results": [{
        "columns": ["graph"],
        "data": [{
            "graph": {
               "nodes": [
                  {
                    id: "1",
                    labels: ["language"],
                    label:'编程语言',
                    from:[],
                    clicked:0,
                    type:'编程语言',
                    properties: {
                      code:"0001"
                    }
                  }
                ],
               "relationships": []
            }
        }]
    }],
   "errors": []
};
// 第二种,D3数据结构，更新数据使用updateWithD3Data
let initJson2={
   "nodes": [
      {
        id: "1",
        labels: ["language"],
        label:'编程语言',
        from:[],
        clicked:0,
        type:'编程语言',
        properties: {
          code:"0001"
        }
      }
    ],
   "relationships": []
            
};


export default {
  name: 'HelloWorld',
  data(){
    return {
      neo4jd3:''
    }
  },
  mounted(){
    this.$nextTick(()=>{
      this.init();
    });
  },
  methods:{
    //初始化
    init(){
       this.neo4jd3= new myNeo4jd3('#neo4jd3', {
            highlight: [//需要高亮显示的节点
                // {
                //     class: 'Project',
                //     property: 'name',
                //     value: 'neo4jd3'
                // }
            ],
            circleLabel:'label',//节点中心显示的字段
            minCollision: 60,
            neo4jData:initJson,//初始节点数据
            //neo4jDataUrl: '../../src/util/neo4jData.json',//静态引用数据文件
            nodeRadius: 25,
            onNodeClick:function(node){//单击更新节点
             console.log(node);
            },
            zoomFit: false//防止自动适应，自动变大
        });
    },
    updateData(){
      this.$nextTick(()=>{
            let testNode={
              nodes:[
                {
                  id:"2",
                  labels:["language2"],
                  label:"高级语言",
                  from:["1"],
                  clicked:0,
                  type:'高级语言',
                  properties:{
                    code:"1110003"
                  }
                },
                {
                  id:"3",
                  labels:["language3"],
                  label:"脚本语言",
                  from:["1"],
                  clicked:0,
                  type:'脚本语言',
                  properties:{
                    code:"1110003"
                  }
                },
                {
                  id:"4",
                  labels:["language4"],
                  label:"PHP",
                  from:["1","3"],
                  clicked:0,
                  type:'PHP',
                  properties:{
                    code:"1110004"
                  }
                },
                {
                  id:"5",
                  labels:["language5"],
                  label:"JavaScript",
                  from:["1","3"],
                  clicked:0,
                  type:'JavaScript',
                  properties:{
                    code:"1110004"
                  }
                },
                {
                  id:"6",
                  labels:["language6"],
                  label:"C",
                  from:["1","2"],
                  clicked:0,
                  type:'C',
                  properties:{
                    code:"1110004"
                  }
                },
                 {
                  id:"7",
                  labels:["language7"],
                  label:"Java",
                  from:["1","2"],
                  clicked:0,
                  type:'Java',
                  properties:{
                    code:"1110004"
                  }
                },
                 {
                  id:"8",
                  labels:["language8"],
                  label:"C++",
                  from:["1","2"],
                  clicked:0,
                  type:'C++',
                  properties:{
                    code:"1110004"
                  }
                }
              ],
              relationships: [ { 
                     id: "10001",
                     type:"computer",
                     startNode: "1",
                     endNode: "2",
                     properties:{},
                     source:"1",
                     target:"2"
                  },
                  { 
                     id: "10002",
                     type:"computer",
                     startNode: "1",
                     endNode: "3",
                     properties:{},
                     source:"1",
                     target:"3"
                  },
                   { 
                     id: "10003",
                     type:"computer",
                     startNode: "3",
                     endNode: "4",
                     properties:{},
                     source:"3",
                     target:"4"
                  },
                   { 
                     id: "10004",
                     type:"computer",
                     startNode: "3",
                     endNode: "5",
                     properties:{},
                     source:"3",
                     target:"5"
                  },
                   { 
                     id: "10005",
                     type:"computer",
                     startNode: "2",
                     endNode: "6",
                     properties:{},
                     source:"2",
                     target:"6"
                  },
                   { 
                     id: "10006",
                     type:"computer",
                     startNode: "2",
                     endNode: "7",
                     properties:{},
                     source:"2",
                     target:"7"
                  },
                   { 
                     id: "10007",
                     type:"computer",
                     startNode: "2",
                     endNode: "8",
                     properties:{},
                     source:"2",
                     target:"8"
                  }
                  ]
            };
            this.neo4jd3.updateWithD3Data(testNode);
        });
    }
  }
}
</script>


<style scoped>
@import "../../src/util/neo4jd3.css";
</style>
