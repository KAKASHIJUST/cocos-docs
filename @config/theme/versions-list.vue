<template>
    <div class="history-version-list">
        <div class="current">Cocos Creator</div>
        <select name="version" :value="currentVersion" @change="changeVersion">
            <option v-for="v in list" :key="v.version" :value="v.version">{{ v.version }}</option>  
        </select>
    </div>
</template>

<script setup lang="js">
import { ref, onMounted } from 'vue';
import { useData } from 'vitepress'
import { langPathMap} from '../config'

const { lang } = useData()

const props = defineProps({
    currentVersion: String
})

const list = ref([]);

onMounted(() => {
    const url = `/creator/versions/versions.json?v=${Date.now()}`;
    fetch(url)
        .then((res) => {
            if(res.ok) {
                res.json().then((data) => {
                    list.value = data;
                });
            }
        })
})

function changeVersion(e) {
    const ver = e.target.value;
    
    if(ver === props.currentVersion) return;

    const goToVersion = list.value.find(v => v.version === ver);

    if(!goToVersion) return;
    
    const link = goToVersion.link || `${window.location.origin}/creator/${ver}/manual/${langPathMap[lang.value]}/`;
    window.location.href = link;

    // hack
    // 如果是新窗口打开其他版本的地址，需要重置一下当前页面的 select (如果是当前页面打开，属于刷新页面，无需处理)
    // 因为 change 之后会改变 select 的 vaule，但是我们只需要它打开其他页面，所以这边的值需要重置会当前的版本
    // e.target.value = props.currentVersion;
}
</script>

<style>
.history-version-list {
    margin-left: 20px;
    display: flex;
    align-items: center;
    & .current {
        background-color: var(--vp-sidebar-bg-color, #f6f6f7);
        padding: 0 12px;
        border-radius: 6px;
    }
    & select {
        margin-left: 4px;
        border: 1px solid var(--vp-c-divider);
        padding: 0 10px;
        min-width: 40px;
        text-align: center;
        border-radius: 6px;
    }
}
/* 针对小屏设备 */
@media (max-width: 480px) {
    .history-version-list {
        margin-left: 10px;
        & .current {
            display: none;
        }
    }
}
</style>