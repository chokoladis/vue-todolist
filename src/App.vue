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
            <input type="number" name="number" >
          </label>
          <label>
            <span>Название</span>
            <input type="text" name="title">
          </label>
          <label>
            <span>Небольшое описание</span>
            <input type="text" name="description">
          </label>
          <label>
            <span>Выполнено</span>
            <input type="checkbox" name="complete">
          </label>
          <button type="button" v-on:click="addTask"
            class="btn btn-outline-success">Сохранить</button>
        </div>
        <ul class="list-group list-group-numbered mt-3">
          <li class="list-group-item d-flex justify-content-between align-items-start">
            <div class="ms-2 me-auto">
              <div class="fw-bold">Subheading</div>
              Cras justo odio
            </div>
            <span class="badge bg-primary rounded-pill">14</span>
          </li>
          <li class="list-group-item d-flex justify-content-between align-items-start">
            <div class="ms-2 me-auto">
              <div class="fw-bold">Subheading</div>
              Cras justo odio
            </div>
            <span class="badge bg-primary rounded-pill">14</span>
          </li>
          <li class="list-group-item d-flex justify-content-between align-items-start">
            <div class="ms-2 me-auto">
              <div class="fw-bold">Subheading</div>
              Cras justo odio
            </div>
            <span class="badge bg-primary rounded-pill">14</span>
          </li>
          <li class="list-group-item d-flex justify-content-between align-items-start">
            <div class="ms-2 me-auto">
              <div class="fw-bold">Subheading</div>
              Cras justo odio
            </div>
            <span class="badge bg-primary rounded-pill">14</span>
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
        tasks: []
      }
    },
    methods:{
      getList(){

      },
      showFormAdd(){
        $('#form_add').addClass('show');
      },
      addTask(){

        // tasks
      }
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

