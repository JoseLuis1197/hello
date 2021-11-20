<template>
  <body>
    <div class="hello">
    
      <b-alert v-model="successfulUserRegistration" variant="success" dismissible>
        Se creó un usuario con éxito.
      </b-alert>
    
      <div>
        <nav class="navbar navbar-light bg-light">
          <div class="container-fluid">
            <a class="navbar-brand">Book shared project</a>
            <span class="navbar-text">
              Comparte tu biblioteca en la comunidad más grande de Perú.
            </span>
            <ul class="nav justify-content-end">
              <li class="nav-item mx-3">
                <b-button
                  @click="modalShowRegister = !modalShowRegister"
                  variant="outline-success"
                  size="sm"
                >
                  Únete</b-button
                >
              </li>
              <li class="nav-item mx-3">
                <b-button
                  variant="success"
                  size="sm"
                  @click="modalShowJoin = !modalShowJoin"
                  >Inicia sesión</b-button
                >
              </li>

              <b-modal
                v-model="modalShowRegister"
                ref="registerModal"
                hide-footer
                title="Regístrate"
              >
                <div class="d-block">
                  <b-form>
                    <b-form-group
                      label="Correo electrónico:"
                      description="Jamás compartiremos tu correo con nadie."
                      valid-feedback="Gracias"
                    >
                      <b-form-input
                        placeholder="Ingresa tu correo"
                        required
                        type="email"
                        v-model="validation.email"                        
                      >                      
                      </b-form-input>
                    </b-form-group>
                    <b-form-group
                      label="Contraseña"
                      description="Tu contraseña debe contener mayúsculas, números y caracteres especiales."
                      valid-feedback="Gracias"
                    >
                      <b-form-input
                        placeholder="Ingresa una constraseña válida"
                        required
                        type="password"
                        v-model="validation.password"
                      >
                      </b-form-input>
                    </b-form-group>
                  </b-form>
                </div>
                <b-button
                  class="mt-2"
                  variant="outline-danger"
                  @click="modalShowRegister = !modalShowRegister"
                  >Regresar</b-button
                >
                <b-button
                  class="mt-2 mx-3"
                  variant="outline-success"
                  @click="createUser()"
                  >Crear usuario</b-button
                >
              </b-modal>

              <b-modal
                ref="joinmodal"
                centered
                title="Inicio de sesión"
                v-model="modalShowJoin"
              >
                <b-container fluid>
                  <div class="form-floating mb-3">
                    <input
                      type="email"
                      class="form-control"
                      id="floatingInput"
                      placeholder="name@example.com"
                    />
                    <label for="floatingInput">Usuario</label>
                  </div>
                  <div class="form-floating">
                    <input
                      type="password"
                      class="form-control"
                      id="floatingPassword"
                      placeholder="Password"
                    />
                    <label for="floatingPassword">Contraseña</label>
                  </div>
                </b-container>

                <template #modal-footer>
                  <b-button
                    variant="success"
                    @click="modalShowJoin = !modalShowJoin"
                  >
                    OK
                  </b-button>
                  <b-button
                    variant="danger"
                    @click="modalShowJoin = !modalShowJoin"
                  >
                    Cancel
                  </b-button>
                </template>
              </b-modal>
            </ul>
          </div>
        </nav>
      </div>

      <div class="container mb-5 mt-5">
        <div class="row align-self-center">
          <div class="col-6">
            <label class="fs-2">Bienvenidos a nuestra comunidad</label>
            <label class="fs-9 text-black-50">
              Podrás compartir los libros que no lees con demás personas e
              intercambiar el conocimiento.
            </label>
            <button type="button" class="btn btn-primary mt-3 text-nowrap">
              <label class="text-white">¡Aprende cómo!</label>
            </button>
          </div>
          <div class="col-6 ps-5">
            <img src="../assets/book_image.jpg" />
          </div>
        </div>
      </div>

      <div class="container mb-5">
        <div class="row">
          <div class="col-sm-4">
            <div class="card border-0">
              <div class="card-body">
                <i
                  class="bi-bookmark"
                  style="font-size: 3rem; color: brown"
                ></i>
                <h5 class="card-title">{{ services[0].name }}</h5>
                <p class="card-text">{{ services[0].description }}</p>
                <a href="#" class="btn btn-outline-primary">Saber más</a>
              </div>
            </div>
          </div>
          <div class="col-sm-4">
            <div class="card border-0">
              <div class="card-body">
                <i class="bi-book" style="font-size: 3rem; color: brown"></i>
                <h5 class="card-title">{{ services[1].name }}</h5>
                <p class="card-text">{{ services[1].description }}</p>
                <a href="#" class="btn btn-outline-primary">Saber más</a>
              </div>
            </div>
          </div>
          <div class="col-sm-4">
            <div class="card border-0">
              <div class="card-body">
                <i
                  class="bi-journals"
                  style="font-size: 3rem; color: brown"
                ></i>
                <h5 class="card-title">{{ services[2].name }}</h5>
                <p class="card-text">{{ services[2].description }}</p>
                <a href="#" class="btn btn-outline-primary">Saber más</a>
              </div>
            </div>
          </div>
        </div>
      </div>
      <footer>
        <div
          class="
            bg-success bg-gradient
            container-fluid
            m-auto
            row
            align-items-end
          "
        >
          <div class="row gx-5">
            <div class="col-6">
              <i
                class="bi bi-book-fill"
                style="font-size: 3rem; color: brown"
              ></i>
              <label class="m-2 fs-2 text-white">The Book Shared Project</label>
            </div>
            <div class="col-3">
              <div class="fs-5 m-2 text-white">Métodos de pago</div>
              <div>
                <img :src="image.visaAddress" class="img-fluid px-1" />
                <img :src="image.mastercardAddress" class="img-fluid px-1" />
                <img :src="image.amexAddress" class="img-fluid px-1" />
                <img :src="image.dinersAddress" class="img-fluid px-1" />
              </div>
            </div>
            <div class="col-3 text-white">
              <div class="fs-5 m-2">Políticas y términos</div>
              <div class="m-1">Términos y condiciones</div>
              <div class="m-1">Condiciones de pago online</div>
            </div>
            <div class="col-12">
              <div class="text-center p-3" style="color: black">
                © 2020 Copyright:
                <a class="text-white" href="https://mdbootstrap.com/"
                  >Book Shared Project</a
                >
              </div>
            </div>
          </div>
        </div>
      </footer>
    </div>
  </body>
</template>

<script>
export default {
  name: "HelloWorld",
  props: {
    msg: String,
  },
  data() {
    return {
      modalShowRegister: false,
      modalShowJoin: false,
      successfulUserRegistration: false,
      image: {
        visaAddress: require("../assets/visa_icon.png"),
        mastercardAddress: require("../assets/mastercard_icon.png"),
        amexAddress: require("../assets/amex_icon.png"),
        dinersAddress: require("../assets/diners_icon.png"),
      },
      services: [
        {
          id: "1",
          name: "Intercambia libros",
          description:
            "Arma tu biblioteca y encuentra quién más es adepto a tus gustos.",
        },
        {
          id: "2",
          name: "Vende tus libros viejos",
          description:
            "No los extrañes! Nuestra comunidad está ansiosa de aprender de ti.",
        },
        {
          id: "3",
          name: "Compra libros viejos",
          description:
            "Compra libros de otras personas y aprender de sus lecturas.",
        },
      ],
      validation: {
        email: "",        
        password: "",
        emailState:false,
        passWordState:""
      },
    };
  },
  methods: {    
    createUser(){
         

      this.modalShowRegister = !this.modalShowRegister,      
      this.successfulUserRegistration = !this.successfulUserRegistration
    }
  },
};
</script>