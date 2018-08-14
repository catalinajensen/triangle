<template>
  <div>
    <header data-ts="TopBar"></header>
    <main data-ts="Main">
      <b-container data-ts="MainContent">
        <h1>Triangle challenge</h1>
        <b-row>
          <div data-ts="Note">
            <p>Enter the lengths of the triangle's 3 sides</p>
          </div>
        </b-row>
        <b-row>
          <form data-ts="Form" @submit="checkTriangle()">
            <b-row>
              <b-col>
                <fieldset>
                  <label :class="{'ts-error': side1.triggered}">
                    <span>Side 1</span>
                    <input name="side1" type="number" min="0" v-model="side1.value" required/>
                  </label>
                  <dl class="ts-errors" v-if="side1.triggered">
                    <dt>Error: {{side1.message}}</dt>
                  </dl>
                </fieldset>
              </b-col>
              <b-col>
                <fieldset>
                  <label :class="{'ts-error': side2.triggered}">
                    <span>Side 2</span>
                    <input name="side2" type="number" min="0" v-model="side2.value" required/>
                  </label>
                  <dl class="ts-errors" v-if="side2.triggered">
                    <dt>Error: {{side2.message}}</dt>
                  </dl>
                </fieldset>
              </b-col>
              <b-col>
                <fieldset>
                  <label :class="{'ts-error': side3.triggered}">
                    <span>Side 3</span>
                    <input name="side3" type="number" min="0" v-model="side3.value" required/>
                  </label>
                  <dl class="ts-errors" v-if="side3.triggered">
                    <dt>Error: {{side3.message}}</dt>
                  </dl>
                </fieldset>
              </b-col>
            </b-row>
            <br>
            <b-row>
              <b-col md="3" offset-md="1">
                <button data-ts="Button" type="submit" class="ts-primary">
                  <span>Check</span>
                </button>
              </b-col>
            </b-row>
          </form>
        </b-row>
      </b-container>
    </main>
  </div>
</template>

<script>
export default {
  name: "LayoutComponent",
  data() {
    return {
      side1: {
        value: "",
        triggered: false,
        message: ""
      },
      side2: {
        value: "",
        triggered: false,
        message: ""
      },
      side3: {
        value: "",
        triggered: false,
        message: ""
      },
      messages: ["Must not be empty!", "Must be a number greater than 0!"]
    };
  },
  watch: { // watch for changes of the input's values
    "side1.value": function() {
      if (this.side1.value <= 0 && this.side1.value !== "") {
        this.side1.triggered = true;
        this.side1.message = this.messages[1];
      } else {
        this.side1.triggered = false;
      }
    },
    "side2.value": function() {
      if (this.side2.value <= 0 && this.side2.value !== "") {
        this.side2.triggered = true;
        this.side2.message = this.messages[1];
      } else {
        this.side2.triggered = false;
      }
    },
    "side3.value": function() {
      if (this.side3.value <= 0 && this.side3.value !== "") {
        this.side3.triggered = true;
        this.side3.message = this.messages[1];
      } else {
        this.side3.triggered = false;
      }
    }
  },
  methods: {
    checkTriangle: function() {

      // check if the input is empty
      if (this.side1.value === "") {
        this.side1.triggered = true;
        this.side1.message = this.messages[0];
      }

      if (this.side2.value === "") {
        this.side2.triggered = true;
        this.side2.message = this.messages[0];
      }

      if (this.side3.value === "") {
        this.side3.triggered = true;
        this.side3.message = this.messages[0];
      }

      // check if none of the inputs are invalid
      if (
        !this.side1.triggered &&
        !this.side2.triggered &&
        !this.side3.triggered
      ) {
        // compare sides
        if (this.side1.value === this.side2.value) {
          if (this.side1.value === this.side3.value) {
            ts.ui.Notification.success("Equilateral triangle");
          } else {
            ts.ui.Notification.success("Isosceles triangle");
          }
        } else if (this.side2.value === this.side3.value) {
          ts.ui.Notification.success("Isosceles triangle");
        } else if (this.side1.value === this.side3.value) {
          ts.ui.Notification.success("Isosceles triangle");
        } else {
          ts.ui.Notification.success("Scalene triangle");
        }
      }
    }
  }
};
</script>

<style lang="scss">

</style>
