<template>
  <div class="home">
  
      <h3 class="pt-4 pl-4">My Daily Tasks : 
        <v-fade-transition leave-absolute>
            <span :key="`tasks-${tasks.length}`">
              {{ tasks.length }}
            </span>
        </v-fade-transition>
      </h3>
      <v-divider class="mt-4"></v-divider>
        <v-row
          class="my-1 pa-4"
          align="center"
        >
          <strong class="mx-4 info--text text--darken-2">
            Remaining: {{ remainingTasks }}
          </strong>

          <v-divider vertical></v-divider>

          <strong class="mx-4 success--text text--darken-2">
            Completed: {{ completedTasks }}
          </strong>

          <v-divider vertical></v-divider>
        
          <v-progress-circular
            :value="progress"
            :size="40"
            color="primary"
            class="ml-4"
            
          ></v-progress-circular>
        </v-row>

      <v-divider class="mb-4"></v-divider>
    
  <v-text-field
            v-model="newTaskTitle"
            @click:append="addTask"
            @keyup.enter="addTask"
            outlined
            label="Add Task"
            append-icon="mdi-plus-thick"
            class="pl-4 pr-4"
            hide-details
            clearable
  ></v-text-field>
    
    <v-subheader>Currently Working on :</v-subheader>
    <v-slide-y-transition
        class="py-0"
        group
      >
     <div  v-for="task in tasks"
          :key="task.id"
          @click="doneTask(task.id)"
          :class= " {'blue lighten-5' : task.done }"
          
          >
        <v-list-item>
          <template v-slot:default>
            <v-list-item-action>
              <v-checkbox 
              :input-value="task.done"
              :color="task.done && 'grey' || 'primary'"></v-checkbox>
            </v-list-item-action>

            <v-list-item-content>
              <v-list-item-title
              :class=" {'text-decoration-line-through' : task.done}"
              >
                {{ task.title }}
              </v-list-item-title>
            </v-list-item-content>
            
            <v-scroll-x-transition>
              <v-icon
                v-if="task.done"
                color="success"
              >
                mdi-check
              </v-icon>
            </v-scroll-x-transition>
      
            <v-list-item-action>
              <v-btn 
              @click.stop="deleteTask(task.id)"
              icon>
                <v-icon color="grey lighten-1">mdi-close-thick</v-icon>
              </v-btn>
            </v-list-item-action>
          </template>
          
        </v-list-item>
        <v-divider></v-divider>
     </div>
    </v-slide-y-transition> 
    <v-snackbar
      v-model="snackbar"
      tile
      :timeout="750"
    >
      {{ text }}

      <template v-slot:action="{ attrs }">
        <v-btn
          color="white"   
          text
          v-bind="attrs"
          @click="snackbar = false"
        >
          Close
        </v-btn>
      </template>
    </v-snackbar>
  </div>
</template>

<script>

  export default {
    name: 'Home',
    data () {
      return { 
        newTaskTitle : null,
        tasks : [], 
        snackbar: false,
        text: null,
      }
    }, 
    methods : {
      doneTask(id){
        let task = this.tasks.filter(task => task.id === id)[0];
        task.done = !task.done;
        if (task.done === true){
          this.text = "Task Completed ! ";
          this.snackbar = true;
        }

      },
      deleteTask(id){
        this.tasks = this.tasks.filter(task => task.id !== id);
        this.text = "Task Removed !";
        this.snackbar = true;
      }, 
      addTask(){
        let newTask = {
          id : Date.now(),
          title : this.newTaskTitle,
          done : false
        }
        // Add task only if it isn't empty
        if (newTask.title !== null) {
            this.tasks.unshift(newTask);
            this.text = "Task Added !";
          this.snackbar = true;
        } 
        this.newTaskTitle = null;
      }
    },
    computed: {
      completedTasks () {
        return this.tasks.filter(task => task.done).length
      },
      progress () {
        if (this.tasks.length !== 0 ) {
            return this.completedTasks / this.tasks.length * 100;
        }else {
          return 0;
        }
        
        
      },
      remainingTasks () {
        return this.tasks.length - this.completedTasks
      },
    },

  }
  
</script>
