<template>
  <nav class="navbar justify-content-between navbar-dark bg-primary mb-4 px-4">
    <RouterLink class="navbar-brand" to="/">知乎</RouterLink>
    <ul v-if="!user.isLogin" class="list-inline mb-0">
      <li class="list-inline-item"><RouterLink to="/login" class="btn btn-outline-light my-2">登录</RouterLink></li>
      <li class="list-inline-item"><RouterLink to="/" class="btn btn-outline-light my-2">注册</RouterLink></li>
    </ul>
    <ul v-else class="list-inline mb-0">
      <!-- <li class="list-inline-item"><a href="#" class="btn btn-outline-light my-2">欢迎：{{user.name}}</a></li> -->
      <li class="list-inline-item">
        <Dropdown :title="`欢迎 ${user.name}`">
          <DropdownItem><router-link class="dropdown-item" to="/create">新建文章</router-link></DropdownItem>
          <DropdownItem :disabled="true"><a class="dropdown-item" href="#">编辑资料</a></DropdownItem>
          <DropdownItem><a class="dropdown-item" href="#" @click="loginOut">退出登录</a></DropdownItem>
        </Dropdown>
      </li>
    </ul>
  </nav>
</template>

<script lang="ts">
import { defineComponent, PropType } from 'vue'
import Dropdown from './Dropdown.vue'
import DropdownItem from './DropdownItem.vue'
import { useRouter } from 'vue-router'

export interface UserProps {
  isLogin: boolean,
  id?: number,
  name?: string,
}

export default defineComponent({
  name: 'GlobalHeader',
  props: {
    user: {
      type: Object as PropType<UserProps>,
      required: true
    }
  },
  components: {
    Dropdown,
    DropdownItem
  },
  setup () {
    // eslint-disable-next-line @typescript-eslint/no-unused-vars
    const router = useRouter()
    const loginOut = () => {
      localStorage.removeItem('token')
    }
    return {
      loginOut
    }
  }
})
</script>

<style scoped>

</style>
