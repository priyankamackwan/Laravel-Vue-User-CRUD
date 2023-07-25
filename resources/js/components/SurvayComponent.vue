<template>
    <div>
      <h3 class="text-success" align="center">Multistep Form In VueJs</h3>
      <br>
      <div class="container" id="survay-app">
         <div class="panel-group">
            <div class="panel panel-primary">
               <div class="panel-heading">Multistep Form In VueJs</div>
                  <fieldset v-if="page == 1">
                     <div class="panel-body">
                        <h4>Step {{ page }}</h4>
                        <br>
                        <div class="form-group" v-for="(question, index) in questions" v-if="index <= 4">
                           <h4> {{ question.question }} </h4>
                           <div class="col-sm-5">
                                <label :for="'question_'+ question.id">1</label>
                                <input type="radio" value="1" v-model="datas['question_'+question.id]" :name="'question_'+ question.id" />
                                <label :for="'question_'+ question.id">2</label>
                                <input type="radio" value="2" v-model="datas['question_'+question.id]" :name="'question_'+ question.id" />
                                <label :for="'question_'+ question.id">3</label>
                                <input type="radio" value="3" v-model="datas['question_'+question.id]" :name="'question_'+ question.id" />
                                <label :for="'question_'+ question.id">4</label>
                                <input type="radio" value="4" v-model="datas['question_'+question.id]" :name="'question_'+ question.id" />
                                <label :for="'question_'+ question.id">5</label>
                                <input type="radio" value="5" v-model="datas['question_'+question.id]" :name="'question_'+ question.id" />
                           </div>
                        </div>
                        <button @click.prevent="next(page)" class="btn btn-primary">Next</button>
                     </div>
                     
                  </fieldset>
                  <fieldset v-if="page == 2">
                    <div class="panel-body">
                       <h4>Step {{ page }}</h4>
                       <br>
                       <div class="form-group" v-for="(question, index) in questions" v-if="index >=5">
                          <h4> {{ question.question }} </h4>
                          <div class="col-sm-5">
                               <label :for="'question_'+ question.id">1</label>
                               <input type="radio" value="1" v-model="datas['question_'+question.id]" :name="'question_'+ question.id" checked />
                               <label :for="'question_'+ question.id">2</label>
                               <input type="radio" value="2" v-model="datas['question_'+question.id]" :name="'question_'+ question.id" />
                               <label :for="'question_'+ question.id">3</label>
                               <input type="radio" value="3" v-model="datas['question_'+question.id]" :name="'question_'+ question.id" />
                               <label :for="'question_'+ question.id">4</label>
                               <input type="radio" value="4" v-model="datas['question_'+question.id]" :name="'question_'+ question.id" />
                               <label :for="'question_'+ question.id">5</label>
                               <input type="radio" value="5" v-model="datas['question_'+question.id]" :name="'question_'+ question.id" />
                          </div>
                       </div>
                       <button  @click.prevent="prev(page)" class="btn btn-info">Previous</button>
                       <button  @click.prevent="submit()" class="btn btn-success">Save</button>
                    </div>
                    
                 </fieldset>
                 <fieldset v-if="page == 3">
                    <div class="panel-body">
                        <table class="table">
                            <thead>
                                <tr>
                                <th>Question</th>
                                <th>answer</th>
                                <th>Avg. answer</th>
                                </tr>
                            </thead>
                            <tbody>
                                <tr>
                                <td></td>
                                <td></td>
                                <td></td>
                                </tr>
                            </tbody>
                          </table>
                    </div>
                 </fieldset>
            </div>
         </div>
      </div>
    </div>
</template>
<script>
    export default {
        props: [
            'user_id'
        ],
        data() {
            return {
                page: 1,
                datas: {
                    question_1: '1',
                    question_2: '1',
                    question_3: '1',
                    question_4: '1',
                    question_5: '1',
                    question_6: '1',
                    question_7: '1',
                    question_8: '1',
                    question_9: '1',
                    question_10: '1'
                },
                questions: [],
                sutvay: [],
            }
        },
        mounted() {
            this.fetchAll()
            console.log('Component mounted.')
        },
        methods: {
            async fetchAll() {
                try {
                   await axios.get(`/api/questions`)
                        .then(res => this.questions = res.data)
                } catch (e) {
                    console.log(e)
                }
            },
            async fetchAnswer() {
                try {
                   await axios.get(`/api/answer?user_id=${this.user_id}`)
                        .then(res => this.survay = res.data)
                } catch (e) {
                    console.log(e)
                }
            },
            prev(page) {
                // this.step--;
                page--;
                this.page = page;
                // this.fetchAll(page)
            },
            next(page) {
                // this.step++;
                // if(page != 1) {
                    page++;
                    this.page = page;
                    // this.fetchAll(page)
                // }
            },  
            submit() {
                this.datas.user_id = this.user_id;
                let method = axios.post
                let url = "/api/questions"
                method(url, this.datas)
                .then(res => {
                    this.fetchAll()
                    this.page = 3;
                    this.fetchAnswer()
                    flash('User Details Created or Updated.', 'success');
                }).catch(e => {
                    // this.allerros = e.response.data.errors
                })
            }
        }
    }
</script>
