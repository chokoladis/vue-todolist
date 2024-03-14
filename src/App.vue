<template>
    <header>
      <div class="container">
        <h3>todolist</h3>
      </div>
    </header>

    <main>
      <div class="container">

        <button type="button" @click="showFormAdd"
          class="btn btn-outline-primary me-2" id="btn-add-form">Добавить</button>
        <button type="button"  @click="changeList"
          :class="{
            'btn-warning': f_changeList,
            'btn-outline-warning': !f_changeList
          }"
          class="btn" id="btn-change-list">Изменить список</button>

        <div class="form hide mt-4 col-12 col-sm-10 col-md-8 col-lg-6 col-xl-3" id="form_add">
          <div class="close" @click="hideFormAdd">
            <i class="bi bi-dash-square"></i>
          </div>
          <label>
              <span>Номер</span>
              <input type="number" name="number" class="form-control"
                  required v-model="number">
              <div id="validateNumber" class="invalid-feedback" style="display: none;"></div>
          </label>
          <label>
              <span>Название</span>
              <input type="text" name="title" class="form-control"
                  required v-model="title">
              <div id="validateTitle" class="invalid-feedback" style="display: none;"></div>
          </label>
          <label>
              <span>Небольшое описание</span>
              <input type="text" name="description" class="form-control"
                  v-model="description">
              <div id="validateDescription" class="invalid-feedback" style="display: none;"></div>
          </label>
          <label class="flex-row">
              <input type="checkbox" name="complete" class="form-check-input me-2"
                  v-model="complete">
              <span>Выполнено</span>            
          </label>
          <button type="button" v-on:click="addTask"
              class="btn btn-outline-success">Сохранить</button>
        </div>
        <div class="form hide mt-4 col-12 col-sm-10 col-md-8 col-lg-6 col-xl-3" id="form_change">
          <div class="close" @click="hideFormChange">
            <i class="bi bi-dash-square"></i>
          </div>
          <label>
              <span>Номер</span>
              <input type="number" name="number" class="form-control" disabled
                  required v-model="number">
              <div id="validateNumber" class="invalid-feedback" style="display: none;"></div>
          </label>
          <label>
              <span>Название</span>
              <input type="text" name="title" class="form-control"
                  required v-model="title">
              <div id="validateTitle" class="invalid-feedback" style="display: none;"></div>
          </label>
          <label>
              <span>Небольшое описание</span>
              <input type="text" name="description" class="form-control"
                  v-model="description">
              <div id="validateDescription" class="invalid-feedback" style="display: none;"></div>
          </label>
          <label class="flex-row">
              <input type="checkbox" name="complete" class="form-check-input me-2"
                  v-model="complete">
              <span>Выполнено</span>            
          </label>
          <button type="button" v-on:click="updateTask"
              class="btn btn-outline-success">Сохранить</button>
        </div>
        <ul class="list-group mt-3">
          <li class="list-group-item d-flex justify-content-between"
            v-for="task in tasks"
            v-bind:key="task">
            {{ task.number }}
            <div class="ms-2 me-auto">
              <div class="fw-bold">{{ task.title }}</div>
              {{ task.description }}
            </div>
            <span class="badge bg-primary rounded-pill" v-if="task.complete">
              <i class="bi bi-check2"></i>
            </span>
            <span class="badge bg-warning rounded-pill" v-else>
              <i class="bi bi-dash"></i>
            </span>
            <div class="change-action" style="display: none;">
              <span class="badge bg-warning rounded-pill"
                @click="editTask(task)">
                <i class="bi bi-pen"></i>
              </span>
              <span class="badge bg-danger rounded-pill"
                @click="deleteTask(task.number)">
                <i class="bi bi-trash2"></i>
              </span>
            </div>
          </li>
        </ul>

      </div>
    </main>

</template>

<style lang="scss">
  @keyframes pulsing {
    0%{
      border: var(--bs-list-group-border-width) solid var(--bs-list-group-border-color);
      transform: rotate(0deg);
    }
    10%{
      transform: rotate(1deg);
    }
    20%{
      border: 1px solid purple;
      transform: rotate(-1deg);
    }
    30%{
      transform: rotate(1deg);
    }
    40%{
      transform: rotate(-1deg)
    }
    50%{
      border: 1px solid rgb(190, 106, 190);
      transform: rotate(1deg);
    }
    60%{
      transform: rotate(-1deg);
    }
    70%{
      border: 1px solid rgb(27, 163, 27);
      transform: rotate(1deg);
    }
    80%{
      transform: rotate(-1deg);
    }
    90%{
      border: 1px solid rgb(106, 172, 106);
      transform: rotate(1deg);
    }
    100%{
      border: var(--bs-list-group-border-width) solid var(--bs-list-group-border-color);
      transform: rotate(0deg);
    }
  }

  *{
    transition-duration: .3s;  
  }

  header{
    padding: 20px 0;

    h3{
      text-transform: uppercase;
      transform: skewX(-10deg);
      text-align: center;
    }
  }

  main{
    .form{
      position: relative;
      padding: 10px;
      padding-top: 20px;
      border-radius: 10px;
      border: 1px solid;
      display: flex;
      flex-direction: column;

      .close{
        position: absolute;
        right: 10px;
        top: 0;
        cursor: pointer;
      }

      label{
        display: flex;
        flex-direction: column;
        margin-bottom: 10px;

      }

      &.hide{
        display: none;
      }
      &.show{
        display: block !important;
      }
    }

    .list-group{
      flex-wrap: wrap;

      .list-group-item{
        align-items: center;

        .badge{
          max-width: 20px;
          display: flex;
          /* align-items: center; */
          justify-content: center;
        }
        
        .change-action{
          display: flex;

          >*{
            cursor: pointer;
            filter: saturate(90%) brightness(90%);
            margin-left: 5px;


            &:hover{
              filter: saturate(100%) brightness(100%);
            }
          }
        }
      }

      &.changes{
        .list-group-item{
          animation: pulsing 3s infinite;
        }
      }
      

      @media screen and (min-width:992px) {
        flex-direction: row;
        
        .list-group-item{
          width: 33%;

          &+.list-group-item{
            border-top-width: var(--bs-list-group-border-width);
            border-left-width: 0;
          }
        }        
      }
    }
  }
</style>

<script>
  export default{
    name: 'App',

    data() {
      return {
        tasks: [],

        number: 0,
        title: '',
        description: '',
        complete: false,

        f_changeList: false
      }
    },
    methods:{
      showFormAdd(){
        $('#form_add').addClass('show');
      },
      hideFormAdd(){
        $('#form_add').removeClass('show');
      },
      hideFormChange(){
        $('#form_change').removeClass('show');
      },
      addTask(){

        let reqFilled = this.isRequiredFill($('#form_add'));

        if (!reqFilled){
          return false;
        }

        let haveThisNumber = this.tasks.find(({ number }) => number == this.number);
        if (haveThisNumber){
          $('#form_add #validateNumber').text('Запись с таким номером есть');
          $('#form_add [name="number"]').addClass('is-invalid');
          $('#form_add #validateNumber').show();
          return false;
        } else {
          $('#form_add #validateNumber').hide();
          $('#form_add [name="number"]').removeClass('is-invalid');
        }

        let newItem = {
          number: this.number,
          title: this.title,
          description: this.description,
          complete: this.complete
        };
        this.tasks.push(newItem);
        this.sortTasks();
        this.clearValues();

      },
      clearValues(){
        this.number = 0;
        this.title = '';
        this.description = '';
        this.complete = false;
      },

      isRequiredFill(form){

        let inputs = form.find('input[required]');
        let fill = true;

        for (let key in inputs){

          if (key === 'length') break;
          
          let value = inputs[key].value;
          if (!value){
            
            $(inputs[key]).addClass('is-invalid');

            fill = false;
          } else {
            $(inputs[key]).removeClass('is-invalid');
          }
        }

        return fill;
      },

      changeList(){

        if (this.f_changeList){

          this.f_changeList = false;
          $('.list-group').removeClass('changes');
          $('.change-action').hide();
          $('#btn-add-form').show();
          $('#form_change').hide();

        } else {

          this.f_changeList = true;
          $('.list-group').addClass('changes');
          $('.change-action').show();
          $('#btn-add-form').hide();
          $('#form_add').removeClass('show');

        }        
      },
      editTask(task){
        this.number = task.number;
        this.title = task.title;
        this.description = task.description;
        this.complete = task.complete;

        $('#form_change').show();
      },
      updateTask(){

        let haveThisNumber = this.tasks.find(( task ) => task.number == this.number);
        if (!haveThisNumber){
          // error epmty
        } else {
          haveThisNumber.number = this.number;
          haveThisNumber.title = this.title;
          haveThisNumber.description = this.description;
          haveThisNumber.complete = this.complete;
        }

        $('#form_change').hide();
      },
      deleteTask(task_number){
        this.tasks = this.tasks.filter(( task ) => task.number != task_number);
      },
      sortTasks(){
        let test = this.tasks.sort((a, b) => { 
          if (a.number < b.number) {
            return -1;
          }
          if (a.number > b.number) {
            return 1;
          }
          return 0;
        });
        this.tasks = test;
      }
    },
    watch:{
      'tasks': function(){
        this.sortTasks();
      }
    }
  }
</script>