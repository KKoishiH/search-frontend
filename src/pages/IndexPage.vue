<template>
  <div class="index-page">
    <a-input-search
      v-model:value="searchParams.text"
      placeholder="input search text"
      enter-button="Search"
      size="large"
      @search="onSearch"
    />
    <MyDivider />
    <a-tabs v-model:activeKey="activeKey" @change="onTagsChange">
      <a-tab-pane key="post" tab="文章">
        <PostList :post-list="postList" />
      </a-tab-pane>
      <a-tab-pane key="picture" tab="图片" force-render>
        <PictureList />
      </a-tab-pane>
      <a-tab-pane key="user" tab="用户">
        <UserList :user-list="userList"/>
      </a-tab-pane>
    </a-tabs>
  </div>
</template>

<script setup lang="ts">
import { ref, watchEffect } from "vue";
import PostList from "@/components/PostList.vue";
import PictureList from "@/components/PictureList.vue";
import UserList from "@/components/UserList.vue";
import MyDivider from "@/components/MyDivider.vue";
import myAxios from "@/plugins/myAxios";
import { useRouter, useRoute } from "vue-router";

// 获取帖子列表
const postList = ref([]);
myAxios.post("/post/list/page/vo", {}).then((res: any) => {
  postList.value = res.records;
});
// 获取用户列表
const userList = ref([]);
myAxios.post("/user/list/page/vo", {}).then((res: any) => {
  userList.value = res.records;
});
const router = useRouter();
// url同步到页面状态(使用route获取到当前页面信息)
const route = useRoute();

const activeKey = route.params.category as string;

const initSearchParams = {
  text: "",
  pageSize: 10,
  pageNum: 1,
};

const searchParams = ref(initSearchParams);
// 传入的一个函数 当依赖项变化的时候 重新执行改函数
watchEffect(() => {
  searchParams.value = {
    ...initSearchParams,
    text: route.query.text,
  } as any;
});

// 搜索内容反映到url
const onSearch = (value: string) => {
  router.push({
    query: searchParams.value,
  });
};
// 切换标签页反映到url
const onTagsChange = (key: string) => {
  router.push({
    path: `/${key}`,
    query: searchParams.value,
  });
};
</script>
