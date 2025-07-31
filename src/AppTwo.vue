<template>
  <table>
    <thead>
      <tr>
        <th>品項</th>
        <th>描述</th>
        <th>價格</th>
        <th>庫存</th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="item in datas" :key="item.id">
        <td>
          <template v-if="item.isEditing">
            <input type="text" v-model="item.tempCategory" />
            <button @click="saveEditCategory(item)">儲存</button>
             <button @click="cancelEditCategory(item)">取消</button>
          </template>
          <template v-else>
             <button @click="editCategory(item)">編輯</button> 
             {{ item.category }}          
          </template>
        </td>
        <td>{{ item.description }}</td>
        <td>{{ item.price }}</td>
        <td>
          <button type="button" @click="decreaseNum(item)">-</button>
        {{ item.inventory }}
          <button type="button" @click="increaseNum(item)">+</button>
        </td>
      </tr>
    </tbody>
  </table>
</template>

<script setup>
import { ref } from 'vue'

const datas = ref([
  { id: '001', category: "珍珠奶茶", description: "香濃奶茶搭配QQ珍珠", price: 50, inventory: 20 ,tempCategory: "珍珠奶茶", isEditing: false },
  { id: '002', category: "冬瓜檸檬", description: "清新冬瓜配上新鮮檸檬", price: 45, inventory: 18, tempCategory: "冬瓜檸檬", isEditing: false },
  { id: '003', category: "翡翠檸檬", description: "綠茶與檸檬的完美結合", price: 55, inventory: 34, tempCategory: "翡翠檸檬", isEditing: false },
  { id: '004', category: "四季春茶", description: "香醇四季春茶，回甘無比", price: 45, inventory: 10, tempCategory: "四季春茶", isEditing: false },
  { id: '005', category: "阿薩姆奶茶", description: "阿薩姆紅茶搭配香醇鮮奶", price: 50, inventory: 25, tempCategory: "阿薩姆奶茶", isEditing: false },
  { id: '006', category: "檸檬冰茶", description: "檸檬與冰茶的清新組合", price: 45, inventory: 20, tempCategory: "檸檬冰茶", isEditing: false },
  { id: '007', category: "芒果綠茶", description: "芒果與綠茶的獨特風味", price: 55, inventory: 18, tempCategory: "芒果綠茶", isEditing: false },
  { id: '008', category: "抹茶拿鐵", description: "抹茶與鮮奶的絕配", price: 60, inventory: 20, tempCategory: "抹茶拿鐵", isEditing: false }
])

// 初始化每筆資料的編輯狀態與暫存名稱
datas.value.forEach(item => {
  item.isEditing = false
  item.tempCategory = item.category
})

const decreaseNum = (item) => {
  if (item.inventory > 0) item.inventory--
}

const increaseNum = (item) => {
  item.inventory++
}

const editCategory = (item) => {
  item.isEditing = true
  item.tempCategory = item.category
}

const saveEditCategory = (item) => {
  if (item.tempCategory.trim() !== "") {
    item.category = item.tempCategory.trim()
  }
  item.isEditing = false
}

const cancelEditCategory = (item) => {
  item.category
  item.isEditing = false
}
</script>
