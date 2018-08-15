<<template>
 <footer>
    <ul class="footer" :style="{background: footerBgColor}">
        <li class="footer-menu" v-for="(menu, index) in menuList" :key="index">
            <router-link @click.native="selectMenu(menu)" :to="menu.path">{{menu.title}}</router-link>
        </li>
    </ul> 
     </footer>
</template>

<script>
export default {
  data() {
    return {
    //   bgColor: ""
    };
  },
  props: ["menuList", "footerBgColor"],

  methods: {
    selectMenu(menu) {
       this.bgColor=menu.bgColor
      this.$emit("changeTitle", menu);
    }
  },
 
  created () {
    
  }
};
</script>
<style lang="scss" scoped>
.footer {
  display: flex;
  position: fixed;
  bottom: 0;
  width: 100%;
  height: 1rem;
  background-color: #e54847;
  &-menu {
    flex-grow: 1;
    text-align: center;
    line-height: 1rem;
    color: #fff;
  }
  a {
      color: #ccc;
      outline: none;
      &.router-link-active {
        color: #fff;
      }
    }
}
</style>
