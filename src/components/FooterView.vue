<template>
  <div class="footer">
    <div class="subscribe">
      <div class="custom-container">
        <div class="row justify-content-between">
          <div class="subscribe-title col-lg-8 col-md-12 col-sm-12 mx-auto">
            <h2>Subscribe and become a part of Choicie</h2>
            <h3>
              Leave your email and get all the information about product updates,
              blog updates, exclusive updates.
            </h3>
          </div>
          <div
            class="col-lg-4 col-md-12 col-sm-12 d-flex flex-column align-items-lg-end align-items-md-center align-items-sm-center align-items-center"
          >
            <input type="email" placeholder="You email" />
            <button>Register to Newsletter</button>
          </div>
        </div>
      </div>
    </div>
    <div class="social">
      <div class="social-element"></div>
      <div class="custom-container">
        <div class="row social-content justify-content-between w-100 mx-auto">
          <div class="social-content__img col-lg-3 col-md-12 col-sm-12 d-flex flex-column p-0">
            <img src="../assets/logo2.svg" alt />
            <p>You know what you choose!</p>
          </div>
          <div class="col-lg-4 col-md-12 col-sm-12 d-flex flex-column">
            <div class="row">
              <div class="col-7 d-flex flex-column text-left pl-0">
                <a href="/">Home</a>
                <a href="/">Universal Menu</a>
                <a href="#" target="blank">How do use</a>
                <a href="#" target="blank">Growth Factor</a>
                <a href="#" target="blank">Contact</a>
                <a href="#" target="blank">Privacy Policy</a>
              </div>
              <div class="col-4 d-flex flex-column text-left pl-0">
                <a href="https://uk-ua.facebook.com/" target="blank">Facebook</a>
                <a href="https://twitter.com/" target="blank">Twitter</a>
                <a href="https://www.instagram.com/" target="blank">Instagram</a>
                <a href="https://www.linkedin.com/" target="blank">LinkedIn</a>
              </div>
            </div>
          </div>
          <form
            action
            class="form col-lg-4 col-md-12 col-sm-12 d-flex flex-column align-items-lg-end align-items-md-center align-items-sm-center align-items-center p-0"
          >
            <input type="text" placeholder="Name" />
            <input type="email" placeholder="Email" />
            <input type="text" placeholder="Enter text" />
            <button type="submit" class="submit">Get Started</button>
            <button type="submit" class="send">Send</button>
          </form>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "FooterView",
  props: {
    msg: String
  }
};
</script>

<style lang="scss" scoped>
@import "../assets/styles.scss";
a {
  font-size: 14px;
  line-height: 24px;
  font-weight: 400;
  color: $white;
  text-decoration: none;
  margin-bottom: 24px;
  &:focus {
    color: $white;
    text-decoration: none;
  }
  &:hover {
    color: $white;
    text-decoration: none;
  }
}
input {
  padding: 14px 60px 14px 24px;
  align-items: center;
  gap: 10px;
  border-radius: 100px;
  border: none;
  background: $bg-dark;
  margin-bottom: 16px;
}
input::placeholder {
  color: white;
  font-size: 16px;

  font-weight: 400;
  line-height: 20px;
}
button {
  padding: 14px 24px;
  align-items: center;
  gap: 10px;
  border-radius: 100px;
  border: none;
  background: $brand-yellow;
  color: $white;
  &:hover {
    background-color: $yellow-focus;
  }
  &:focus {
    background-color: $yellow-focus;
  }
  &:disabled {
    color: $brand-yellow;
    background: $yellow-disabled;
  }
}
.send {
  color: $black;
}
.social {
  padding-top: 120px;
  padding-bottom: 163px;
  background-color: $footer-bg;
  color: $white;
  overflow: hidden;

  position: relative;
  &-content {
    & img {
      width: 174px;
    }
    z-index: 1;
    & input {
      width: 298px;
      background: $drpurple-nav;
    }
    & button {
      width: 298px;
    }
    & p {
      font-size: 12px;
      margin-top: 16px;
    }
  }
  &-element {
    position: absolute;
    top: -28%;
    left: 63%;
    z-index: 1;
    background-image: url("../assets/cover.svg");
    background-size: cover;
    width: 761.023px;
    height: 745.681px;
    transform: rotate(4deg);
  }
}

.subscribe {
  background-color: $bg-dark;
  color: $white;
  padding: 70px 0 86px 0;
  &-title {
    margin-right: 30px;
  }
  & input {
    width: 370px;
    border: 1px solid $drpurple-nav;
  }
  & button {
    width: 370px;
  }
  & h3 {
    font-weight: 400;
  }
}
@media screen and (min-width: 320px) and (max-width: 767px) {
  a {
    color: $white;
    margin-bottom: 12px;
  }
  .social {
    padding-bottom: 126px;
    padding-top: 48px;
    &-element {
      top: 24rem;
      left: 5rem;
      width: 367.913px;
      height: 360.497px;
    }
    &-content {
      z-index: 1;
      & img {
        width: 121px;
      }
      & input {
        width: 288px;
        background: $bg-dark;
        &::placeholder {
          font-size: 12px;
          line-height: 20px;
        }
      }
      & input::placeholder {
        color: white;
      }
      & button {
        width: 288px;
      }
      & form {
        margin-top: 37px;
        & .send {
          display: none;
        }
        .submit {
          font-size: 12px;

          line-height: 18px;
        }
      }
      &__img {
        margin-bottom: 36px;
        & p {
          margin-bottom: 0;
        }
      }
      &-element {
        top: -25%;
        left: 20%;
        width: 367.913px;
        height: 360.497px;
      }
    }
  }
  .subscribe {
    padding: 48px 0 50px 0;
    & h2 {
      font-size: 18px;

      line-height: 24px;
    }
    & h3 {
      font-size: 12px;
      margin-bottom: 0;
      font-weight: 400;
      line-height: 20px;
    }
    & input {
      margin-top: 24px;
      width: 288px;
      &::placeholder {
        font-size: 12px;

        line-height: 20px;
      }
    }
    & button {
      width: 288px;
      font-size: 14px;
    }
  }
}
@media screen and (min-width: 768px) and (max-width: 1200px) {
  .subscribe {
    & input {
      margin-top: 24px;
    }
    & h2 {
      font-size: 18px;

      line-height: 24px;
    }
    & h3 {
      font-size: 12px;

      font-weight: 400;
      line-height: 20px;
    }
  }
  .social {
    &-content {
      &__img {
        margin-bottom: 36px;
      }
    }

    & form {
      margin-top: 49px;
      & .send {
        display: none;
      }
    }
    &__img {
      margin-bottom: 36px;
    }
  }
}
@media screen and (min-width: 1200px) {
  .submit {
    display: none;
  }
}
</style>
