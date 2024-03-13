<template>
    <header>
      <div class="container">
        <h3>todolist</h3>
      </div>
    </header>

    <main>
      <div class="container">

        <button type="button" v-on:click="showFormAdd"
          class="btn btn-outline-primary me-2">Добавить</button>
        <button type="button" class="btn btn-outline-warning">Изменить список</button>
        <!-- <button type="button" class="btn btn-outline-success">Success</button> -->

        <div class="form hide mt-4 col-12 col-sm-10 col-md-8 col-lg-6 col-xl-3" id="form_add">
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
        <ul class="list-group mt-3">
          <li class="list-group-item d-flex justify-content-between align-items-start"
            v-for="task in tasks"
            v-bind:key="task">
            {{ task.number }}
            <div class="ms-2 me-auto">
              <div class="fw-bold">{{ task.title }}</div>
              {{ task.description }}
            </div>
            <span class="badge bg-primary rounded-pill" v-if="task.complete">+</span>
            <span class="badge bg-warning rounded-pill" v-else>-</span>            
          </li>
        </ul>

      </div>
    </main>

</template>

<script>
  export default{
    name: 'App',

    data() {
      return {
        tasks: [],
        number: 0,
        title: '',
        description: '',
        complete: false
      }
    },
    methods:{
      showFormAdd(){
        $('#form_add').addClass('show');
      },
      addTask(){

        let reqFilled = this.isRequiredFill($('#form_add'));

        if (!reqFilled){
          return false;
        }

        let haveThisTitle = this.tasks.find(({ title }) => title == this.title);
        if (haveThisTitle){
          $('#form_add #validateTitle').text('Запись с таким заголовком есть');
          $('#form_add [name="title"]').addClass('is-invalid');
          $('#form_add #validateTitle').show();
          return false;
        } else {
          $('#form_add #validateTitle').hide();
          $('#form_add [name="title"]').removeClass('is-invalid');
        }

        let newItem = {
          number: this.number,
          title: this.title,
          description: this.description,
          complete: this.complete
        };
        this.tasks.push(newItem);
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

      // changeList(){

      // },
      // deleteTask(){

      // },
      // changeTask(){

      // }
    }
  }
</script>

<style lang="scss">
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

      padding: 10px;
      border-radius: 10px;
      border: 1px solid;
      display: flex;
      flex-direction: column;

      label{
        display: flex;
        flex-direction: column;
        margin-bottom: 10px;

        // &:last-of-type{
        //   margin: 0;
        // }
        // width: fit-content;
      }

      &.hide{
        display: none;
      }
      &.show{
        display: block !important;
      }

      // &#form_add{
        
      // }
    }

    .list-group{
      flex-wrap: wrap;

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

