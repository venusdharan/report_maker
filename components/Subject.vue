<template>
    <div>
        <v-row>
            <v-col>
                 <v-expansion-panels>
                        <v-expansion-panel>
                        <v-expansion-panel-header>
                            <strong v-if="subject_name">{{subject_name}}</strong>
                            <strong v-else>No Subject Name</strong>
                            
                            <v-spacer></v-spacer>
                            <v-btn @click="remove_this" x-small text style="max-width:60px; margin-left:30px;">Remove</v-btn>
                        </v-expansion-panel-header>
                        <v-expansion-panel-content>
                            <v-text-field
                                label="Subject Name"
                                v-model="subject_name"
                            ></v-text-field>
                            <v-row>
                            
                                <v-col>
                                        <h5>Attendence</h5>
                                        <v-simple-table style="height:200px; overflow-y:scroll;">
                                        <template v-slot:default>
                                        <thead>
                                            <tr>
                                            <th class="text-left">
                                                Name (Week/Month)
                                            </th>
                                            <th class="text-left">
                                                Value
                                            </th>
                                            <th class="text-left">
                                                Operations
                                            </th>
                                            </tr>
                                        </thead>
                                        <tbody>
                                            <tr
                                            v-for="(item,index) in attendence"
                                            :key="index"
                                            >
                                            <td>{{ item.label }}</td>
                                            <td>{{ item.value }}</td>
                                            <td><v-btn text x-small @click="remove_attendence(index)">X</v-btn></td>
                                            </tr>
                                        </tbody>
                                        </template>
                                    </v-simple-table>
                               

                                   <v-text-field
                                    label="Name (Week/Month)"
                                    v-model="att_name"
                                    ></v-text-field> 
                                    <v-text-field
                                    label="Value"
                                    v-model="att_val"
                                    ></v-text-field>
                                    <v-btn x-small @click="add_attendence">ADD</v-btn>
                                </v-col>
                            </v-row>
                            <v-row>
                                <v-col>
                                    <h5>Exams Results</h5>
                                     <v-text-field
                                    label="Exam Total Marks"
                                    v-model="exam_total"
                                    ></v-text-field>
                                     <v-simple-table style="height:200px; overflow-y:scroll;">
                                        <template v-slot:default>
                                        <thead>
                                            <tr>
                                            <th class="text-left">
                                                Name
                                            </th>
                                            <th class="text-left">
                                                Value
                                            </th>
                                            <th class="text-left">
                                                Operations
                                            </th>
                                            </tr>
                                        </thead>
                                        <tbody>
                                            <tr
                                            v-for="(item,index) in exams"
                                            :key="index"
                                            >
                                            <td>{{ item.label }}</td>
                                            <td>{{ item.value }}</td>
                                            <td><v-btn text x-small @click="remove_exam(index)">X</v-btn></td>
                                            </tr>
                                        </tbody>
                                        </template>
                                    </v-simple-table>
                                
                                   <v-text-field
                                    label="Name"
                                    v-model="ex_name"
                                    ></v-text-field> 
                                    <v-text-field
                                    label="Value"
                                    v-model="ex_val"
                                    ></v-text-field>
                                    <v-btn x-small @click="add_exam">ADD</v-btn>
                                </v-col>
                            </v-row>

                             <v-item-group>
                                 <h5>Teacher Evaluation</h5>
                                 <v-item>
                                     <v-slider
                                        v-model="attention"
                                        label="Attendance"
                                        max="100"
                                        thumb-label="always"
                                        ></v-slider>
                                 </v-item>
                                 <v-item>
                                     <v-slider
                                        v-model="punctual"
                                        label="Puntual"
                                        max="100"
                                        thumb-label="always"
                                        ></v-slider>
                                 </v-item>
                                 <v-item>
                                     <v-slider
                                        v-model="assignment"
                                        label="Assignment"
                                        max="100"
                                        thumb-label="always"
                                        ></v-slider>
                                 </v-item>
                             </v-item-group>
                              <v-textarea
                                solo
                                name="input-7-4"
                                label="Comment"
                                v-model="comment"
                                ></v-textarea>
                        </v-expansion-panel-content>
                        </v-expansion-panel>
                    </v-expansion-panels>
            </v-col>
        </v-row>
    </div>
</template>

<script>
export default {
    name:"subject",
    data() {
        return {
           subject_name:"",
           attention:"",
           punctual:"",
           assignment : "",
           attendence:[],
           exams:[],
           att_name:"",
           att_val:"",
           ex_name:"",
           ex_val:"",
           comment:"",
           exam_total:""
        };
    },
    methods:{
        remove_this(){
            this.$emit('remove', this.index);
        },
        get_data(){
            var data = {
                subject_name : this.subject_name,
                attention:this.attention,
                punctual:this.punctual,
                assignment:this.assignment,
                comment:this.comment,
                exams:this.exams,
                attendence:this.attendence,
                exam_total:this.exam_total
            };

            return data;
        },
        add_exam(){
            this.exams.push({
               label:this.ex_name,
                value: parseInt(this.ex_val)
            });
        },
        add_attendence(){
            this.attendence.push({
                label:this.att_name,
                value:this.att_val
            });
        },
        remove_exam(index){
            this.exams.splice(index,1);
        },
        remove_attendence(index){
            this.attendence.splice(index,1);
        }
    },
    props:["index"]
}
</script>