<template>
  <v-app id="inspire">
    <v-content>
      <v-container
      class="fill-height"
      fluid>
        <v-row
          align="center"
          justify="center"
        >
          <div id="title">
            <div style="position:relative;
                        width:500px; margin:0 auto;"
            class="title"
            >
              <h1>
                计算机职业生涯规划
              </h1>
            </div>
          </div>
        </v-row>
      </v-container>
    </v-content>
    
    <v-content>
      <v-container
        class="fill-height"
        fluid
      >
        <v-row
          align="center"
          justify="center"
        >
          <div id="description">
            <div style="position:relative;
                        width:500px; margin:0 auto;"
            class="grey--text"
            >
              本项目旨在帮助初入计算机专业的同学们规划自己将来的职业生涯。
              输入你感兴趣的计算机职业（硬件、前端、数据库乃至全栈工程师）
              点击查询，即可得到该职业需要的技能树，也可以了解到就业方向和
              薪资水平等信息。希望这些信息可以帮助计算机专业的同学们更好地
              综合规划自己的职业生涯。
            </div>
          </div>
          <v-col
            cols="12"
            sm="8"
            md="4"
          >
            <v-card class="elevation-12">
              <v-toolbar
                color="primary"
                dark
                flat
              >
                <v-toolbar-title>我想成为</v-toolbar-title>
                <v-spacer></v-spacer>
                <v-tooltip bottom>
                  <template v-slot:activator="{ on }">
                    <v-btn
                      :href="source"
                      icon
                      large
                      target="_blank"
                      v-on="on"
                    >
                      <v-icon>mdi-code-tags</v-icon>
                    </v-btn>
                  </template>
                  <span>Source</span>
                </v-tooltip>
              </v-toolbar>
              <v-card-text>
                <v-form>
                  <v-text-field v-model="query"
                    label="一个什么样的人"
                    
                    type="text"
                  ></v-text-field>
                </v-form>
              </v-card-text>
              <v-card-actions>
                <v-spacer></v-spacer>
                <v-btn color="primary" @click="clickHandler" >查询</v-btn>
              </v-card-actions>
            </v-card>
          </v-col>
        </v-row>
      </v-container>
    </v-content>
  </v-app>
</template>

<script>
import Bmob from "hydrogen-js-sdk";
  export default {
    props: {
      source: String,
    },
    data(){
      return{
        query:''
      }
    },
    methods:{
      clickHandler(){
        console.log('clk');//测试语句
        if(this.query==''){
          console.log('null');
        }
        else{
          const query = Bmob.Query('Article');
          query.equalTo("name","==",this.query);
            query.find().then(res => {
                this.$store.commit("setName",res[0].text);
            }).catch(err => {
                console.log(err)
            });
            console.log(query)
          this.$router.push("/query/"+this.query);
        }
      }
    }
  }
</script>