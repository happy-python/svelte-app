<script>
    import { cards } from "./store";
    import dayjs from "dayjs";
    import saveAs from "file-saver";

    // 标题
    let title;
    // 内容
    let content;

    // 增加卡片
    function add() {
        // 校验
        if (!title || !content) {
            alert("标题和内容必填！");
            return;
        }

        // 更新卡片状态，追加一个新卡片
        cards.update((item) => {
            return [
                ...item,
                {
                    title,
                    content,
                    createTime: dayjs().format("YYYY-MM-DD HH:mm:ss"),
                },
            ];
        });

        title = "";
        content = "";
    }

    // 导出笔记
    function doExport() {
        const texts = [];
        // 读取 cards 状态数组
        for (const card of $cards) {
            let text = `### ${card.title}\n${card.content}\n${card.createTime}\n`;
            texts.push(text);
        }
        // 写入文件
        const blob = new Blob(texts, { type: "text/plain;charset=utf-8" });
        saveAs(blob, "read_notes.md");
    }
</script>

<style>
    .add-card {
        position: fixed;
        bottom: 0;
        left: 0;
        width: 100%;
        box-sizing: border-box;
        padding: 1rem;
        background-image: linear-gradient(135deg, #fec163 10%, #de4313 100%);
        display: flex;
    }

    .input-wrapper {
        flex: 4; /* 使用 Flex 布局 */
    }

    .input-title {
        width: 100%;
    }

    .input-content {
        width: 100%;
        resize: none;
    }

    .add-btn,
    .export-btn {
        flex: 1;
        margin-left: 1rem;
        color: #666;
    }
</style>

<main>
    <div class="add-card">
        <div class="input-wrapper">
            <input
                class="input-title"
                type="text"
                placeholder="输入标题"
                bind:value={title} />
            <textarea
                class="input-content"
                placeholder="输入内容"
                bind:value={content} />
        </div>
        <button class="add-btn" on:click={add}>添加</button>
        <button class="export-btn" on:click={doExport}>导出</button>
    </div>
</main>
