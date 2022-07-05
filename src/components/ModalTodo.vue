<template>
    <div class='modal_container'>
        <el-dialog :title="todo.todoName" :visible.sync="outerVisible">
            <div class="main_modal-detail">
                <div class="main_left">
                    <div class="main_left-des">
                        <h3>Description</h3>
                        <textarea disabled class="main_left-textarea" v-model="todo.description"></textarea>
                    </div>
                    <div class="main_left-list"></div>
                </div>
                <div class="main_right">
                    <ButtonDetail nameBtn="change name" icon="el-icon-user" @click="innerVisible = true" />
                    <ButtonDetail nameBtn="Label" icon="el-icon-paperclip" />
                    <ButtonDetail nameBtn="Date" icon="el-icon-timer" />
                    <ButtonDetail nameBtn="CheckList" icon="el-icon-document" />
                    <ButtonDetail nameBtn="Delete" icon="el-icon-delete" />
                </div>
            </div>
            <el-dialog v-if="nameBtn === 'change name'" width="30%" :title="nameBtn" :visible.sync="innerVisible"
                append-to-body>
                <input type="text" v-model="changeName" class="input-update" />
                <button class="btn-update" @click="handleChangeName">Update</button>
                <button class="btn-cancel" @click="handleCloseChangeName">Cancel</button>
            </el-dialog>
            <el-dialog v-else-if="nameBtn === 'Delete'" width="30%" :title="nameBtn" :visible.sync="innerVisible"
                append-to-body>
                <p>Do you want delete?</p>
                <button class="btn-update" @click="handleCloseChangeName">Cancel</button>
                <button class="btn-cancel" @click="handleDeleteTodo">Delete</button>
            </el-dialog>
        </el-dialog>
    </div>
</template>

<script>
import { EventBus } from '../EventBus'
import ButtonDetail from './common/ButtonDetail.vue'
export default {
    name: "ModalTodo",
    created() {
        EventBus.$on('open-modal', todo => {
            this.outerVisible = true;
            this.todo = todo.todo;
            this.changeName = todo.todo.todoName;
            this.indCard = todo.indCard;
            this.indTodo = todo.indTodo;
        });
        EventBus.$on('open-modal-in-detail', nameBtn => {
            this.innerVisible = true;
            this.nameBtn = nameBtn
        });
    },
    data() {
        return {
            outerVisible: false,
            innerVisible: false,
            todo: {},
            nameBtn: '',
            changeName: '',
            indCard: 0,
            indTodo: 0,
        };
    },
    methods: {
        handleChangeName() {
            this.todo.todoName = this.changeName;
            this.innerVisible = false;
            this.changeName = "";
        },
        handleCloseChangeName() {
            this.innerVisible = false;
            this.changeName = this.todo.todoName;
        },
        handleDeleteTodo() {
            EventBus.$emit('delete-todo', { indCard: this.indCard, indTodo: this.indTodo });
            this.innerVisible = false;
            this.outerVisible = false;
        }
    },
    components: {
        ButtonDetail
    }
}
</script>

<style scoped>
.modal_container {}

.main_modal-detail {
    display: flex;
}

.main_left {
    margin-top: -30px;
}

.main_right {
    display: flex;
    justify-content: start;
    align-items: center;
    flex-direction: column;
    justify-content: center;
    margin-left: 40px;
}

.main_left-textarea {
    width: 30vw;
    height: 60px;
}

.input-update {
    width: 250px;
    height: 24px;
}

.btn-update {
    margin: 0 5px;
    padding: 7px 10px;
    background-color: rgb(13, 169, 13);
    color: #fff;
    border: none;
    border-radius: 3px;
}
</style>