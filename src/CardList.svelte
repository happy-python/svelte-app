<script>
    import { cards } from "./store";
    // 标题
    export let title;
    // 内容
    export let content;
    // 创建日期
    export let createTime;
    // 卡片序号
    export let index = 0;

    // 删除卡片
    function del() {
        cards.update((item) => {
            item.splice(index, 1);
            return item;
        });
    }
</script>

<style>
    .card {
        padding: 1rem;
        margin: 1rem;
        color: #fff;
        border-radius: 0.5rem;
    }

    .card .title {
        font-weight: bold;
        font-size: 1.2rem;
    }

    .card .content {
        margin: 0.5rem 0;
    }

    .card .creationTime {
        font-size: 0.8rem;
    }

    .del-btn {
        float: right;
        user-select: none;
        opacity: 0;
        transition-duration: 500ms;
    }

    .card:hover .del-btn {
        opacity: 1;
    }
</style>

<main>
    <div class={`card bg-color-${index % 5}`}>
        <div class="title">
            {title}
            <span class="del-btn" on:click={del}>x</span>
        </div>
        <div class="content">{content}</div>
        <div class="creationTime">{createTime}</div>
    </div>
</main>
