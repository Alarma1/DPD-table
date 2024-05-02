<template>
    <div class="table-container">
        <div class="table-container__controls">
            <input class="table-container__input" type="text" @input="searchTerm($event.target.value)"
                   placeholder="Поиск..." :value="inputValue">
            <select class="table-container__select" name="" id="" @change="elementsPerPage($event.target.value)"
                    :value="itemsPerPage">
                <option value="5">5</option>
                <option value="10">10</option>
                <option value="15">15</option>
                <option value="20">20</option>
            </select>
        </div>
        <table class="table-container__table">
            <thead>
            <tr>
                <th class="table-container__th">Аватар</th>
                <th class="table-container__th" @click="sortElements('fio')">
                    <div class="header-content">
                        <span class="header-content-text">ФИО</span>
                        <svg v-if="columnName !== 'fio'" xmlns="http://www.w3.org/2000/svg"
                             fill="none"
                             viewBox="0 0 24 24" stroke-width="1.5"
                             stroke="currentColor" class="header-content-svg">
                            <path stroke-linecap="round" stroke-linejoin="round"
                                  d="M3.75 5.25h16.5m-16.5 4.5h16.5m-16.5 4.5h16.5m-16.5 4.5h16.5"/>
                        </svg>
                        <svg v-if="ascendingOrder === 1 && columnName === 'fio'" xmlns="http://www.w3.org/2000/svg"
                             fill="none"
                             viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="header-content-svg">
                            <path stroke-linecap="round" stroke-linejoin="round"
                                  d="M3 4.5h14.25M3 9h9.75M3 13.5h5.25m5.25-.75L17.25 9m0 0L21 12.75M17.25 9v12"/>
                        </svg>
                        <svg v-if="ascendingOrder === 0 && columnName === 'fio'" xmlns="http://www.w3.org/2000/svg"
                             fill="none"
                             viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="header-content-svg">
                            <path stroke-linecap="round" stroke-linejoin="round"
                                  d="M3 4.5h14.25M3 9h9.75M3 13.5h9.75m4.5-4.5v12m0 0-3.75-3.75M17.25 21 21 17.25"/>
                        </svg>
                    </div>
                </th>
                <th class="table-container__th" @click="sortElements('gender')">
                    <div class="header-content">
                        <span class="header-content-text">Пол</span>
                        <svg v-if="columnName !== 'gender'" xmlns="http://www.w3.org/2000/svg"
                             fill="none"
                             viewBox="0 0 24 24" stroke-width="1.5"
                             stroke="currentColor" class="header-content-svg">
                            <path stroke-linecap="round" stroke-linejoin="round"
                                  d="M3.75 5.25h16.5m-16.5 4.5h16.5m-16.5 4.5h16.5m-16.5 4.5h16.5"/>
                        </svg>
                        <svg v-if="ascendingOrder === 1 && columnName === 'gender'" xmlns="http://www.w3.org/2000/svg"
                             fill="none"
                             viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="header-content-svg">
                            <path stroke-linecap="round" stroke-linejoin="round"
                                  d="M3 4.5h14.25M3 9h9.75M3 13.5h5.25m5.25-.75L17.25 9m0 0L21 12.75M17.25 9v12"/>
                        </svg>
                        <svg v-if="ascendingOrder === 0 && columnName === 'gender'" xmlns="http://www.w3.org/2000/svg"
                             fill="none"
                             viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="header-content-svg">
                            <path stroke-linecap="round" stroke-linejoin="round"
                                  d="M3 4.5h14.25M3 9h9.75M3 13.5h9.75m4.5-4.5v12m0 0-3.75-3.75M17.25 21 21 17.25"/>
                        </svg>
                    </div>
                </th>
                <th class="table-container__th" @click="sortElements('location')">
                    <div class="header-content">
                        <span class="header-content-text">Страна</span>
                        <svg v-if="columnName !== 'location'" xmlns="http://www.w3.org/2000/svg" fill="none"
                             viewBox="0 0 24 24" stroke-width="1.5"
                             stroke="currentColor" class="header-content-svg">
                            <path stroke-linecap="round" stroke-linejoin="round"
                                  d="M3.75 5.25h16.5m-16.5 4.5h16.5m-16.5 4.5h16.5m-16.5 4.5h16.5"/>
                        </svg>
                        <svg v-if="ascendingOrder === 1 && columnName === 'location'" xmlns="http://www.w3.org/2000/svg"
                             fill="none"
                             viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="header-content-svg">
                            <path stroke-linecap="round" stroke-linejoin="round"
                                  d="M3 4.5h14.25M3 9h9.75M3 13.5h5.25m5.25-.75L17.25 9m0 0L21 12.75M17.25 9v12"/>
                        </svg>
                        <svg v-if="ascendingOrder === 0 && columnName === 'location'" xmlns="http://www.w3.org/2000/svg"
                             fill="none"
                             viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="header-content-svg">
                            <path stroke-linecap="round" stroke-linejoin="round"
                                  d="M3 4.5h14.25M3 9h9.75M3 13.5h9.75m4.5-4.5v12m0 0-3.75-3.75M17.25 21 21 17.25"/>
                        </svg>
                    </div>
                </th>
                <th class="table-container__th" @click="sortElements('dateBirth')">
                    <div class="header-content">
                        <span class="header-content-text">Дата рождения</span>
                        <svg v-if="columnName !== 'dateBirth'" xmlns="http://www.w3.org/2000/svg" fill="none"
                             viewBox="0 0 24 24" stroke-width="1.5"
                             stroke="currentColor" class="header-content-svg">
                            <path stroke-linecap="round" stroke-linejoin="round"
                                  d="M3.75 5.25h16.5m-16.5 4.5h16.5m-16.5 4.5h16.5m-16.5 4.5h16.5"/>
                        </svg>
                        <svg v-if="ascendingOrder === 1 && columnName === 'dateBirth'"
                             xmlns="http://www.w3.org/2000/svg" fill="none"
                             viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="header-content-svg">
                            <path stroke-linecap="round" stroke-linejoin="round"
                                  d="M3 4.5h14.25M3 9h9.75M3 13.5h5.25m5.25-.75L17.25 9m0 0L21 12.75M17.25 9v12"/>
                        </svg>
                        <svg v-if="ascendingOrder === 0 && columnName === 'dateBirth'"
                             xmlns="http://www.w3.org/2000/svg" fill="none"
                             viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="header-content-svg">
                            <path stroke-linecap="round" stroke-linejoin="round"
                                  d="M3 4.5h14.25M3 9h9.75M3 13.5h9.75m4.5-4.5v12m0 0-3.75-3.75M17.25 21 21 17.25"/>
                        </svg>
                    </div>
                </th>
                <th class="table-container__th" @click="sortElements('email')">
                    <div class="header-content">
                        <span class="header-content-text">Адрес электронной почты</span>
                        <svg v-if="columnName !== 'email'" xmlns="http://www.w3.org/2000/svg" fill="none"
                             viewBox="0 0 24 24" stroke-width="1.5"
                             stroke="currentColor" class="header-content-svg">
                            <path stroke-linecap="round" stroke-linejoin="round"
                                  d="M3.75 5.25h16.5m-16.5 4.5h16.5m-16.5 4.5h16.5m-16.5 4.5h16.5"/>
                        </svg>
                        <svg v-if="ascendingOrder === 1 && columnName === 'email'" xmlns="http://www.w3.org/2000/svg"
                             fill="none"
                             viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="header-content-svg">
                            <path stroke-linecap="round" stroke-linejoin="round"
                                  d="M3 4.5h14.25M3 9h9.75M3 13.5h5.25m5.25-.75L17.25 9m0 0L21 12.75M17.25 9v12"/>
                        </svg>
                        <svg v-if="ascendingOrder === 0 && columnName === 'email'" xmlns="http://www.w3.org/2000/svg"
                             fill="none"
                             viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="header-content-svg">
                            <path stroke-linecap="round" stroke-linejoin="round"
                                  d="M3 4.5h14.25M3 9h9.75M3 13.5h9.75m4.5-4.5v12m0 0-3.75-3.75M17.25 21 21 17.25"/>
                        </svg>
                    </div>
                </th>
                <th class="table-container__th" @click="sortElements('phone')">
                    <div class="header-content">
                        <span class="header-content-text">Телефон</span>
                        <svg v-if="columnName !== 'phone'" xmlns="http://www.w3.org/2000/svg" fill="none"
                             viewBox="0 0 24 24" stroke-width="1.5"
                             stroke="currentColor" class="header-content-svg">
                            <path stroke-linecap="round" stroke-linejoin="round"
                                  d="M3.75 5.25h16.5m-16.5 4.5h16.5m-16.5 4.5h16.5m-16.5 4.5h16.5"/>
                        </svg>
                        <svg v-if="ascendingOrder === 1 && columnName === 'phone'" xmlns="http://www.w3.org/2000/svg"
                             fill="none"
                             viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="header-content-svg">
                            <path stroke-linecap="round" stroke-linejoin="round"
                                  d="M3 4.5h14.25M3 9h9.75M3 13.5h5.25m5.25-.75L17.25 9m0 0L21 12.75M17.25 9v12"/>
                        </svg>
                        <svg v-if="ascendingOrder === 0 && columnName === 'phone'" xmlns="http://www.w3.org/2000/svg"
                             fill="none"
                             viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="header-content-svg">
                            <path stroke-linecap="round" stroke-linejoin="round"
                                  d="M3 4.5h14.25M3 9h9.75M3 13.5h9.75m4.5-4.5v12m0 0-3.75-3.75M17.25 21 21 17.25"/>
                        </svg>
                    </div>
                </th>
            </tr>
            </thead>
            <tbody>
            <tr v-for="client in arrData" :key="client.id.value">
                <td class="table-container__td"><img class="table-container__avatar" :src="client.picture.medium"
                                                     alt="Аватар"/></td>
                <td class="table-container__td">{{ client.name.title }}
                    {{ client.name.first }}
                    {{ client.name.last }}
                </td>
                <td class="table-container__td">{{ client.gender }}</td>
                <td class="table-container__td">{{ client.location.city }}</td>
                <td class="table-container__td">{{ dateFormat(client.dob.date) }}</td>
                <td class="table-container__td">{{ client.email }}</td>
                <td class="table-container__td">{{ client.phone }}</td>
            </tr>
            </tbody>
        </table>

        <div class="pagination">
            <button @click="prevPage" :disabled="currentPage === 1"
                    class="pagination__button">Пред.
            </button>
            <button @click="selectPage(page)"
                    v-for="(page, index) in totalPages" :key="index"
                    :class="{'select-page': page === currentPage}"
                    class="pagination__button">{{ page }}
            </button>
            <button @click="nextPage" :disabled="currentPage === totalPages">След.</button>
        </div>
    </div>
</template>

<script setup>
    import ApiJson from '../Api/api.json'
    import {ref, onMounted} from "vue";
    import {useRouter} from 'vue-router'

    const clientsData = ApiJson.results
    const inputValue = ref('')
    const currentPage = ref(1)
    const itemsPerPage = ref(5)
    const arrData = ref([])
    const clientsDataCopy = ref([])
    const ascendingOrder = ref(2)
    const totalPages = ref(1)
    const clientsDataCopySortElements = ref([])
    const columnName = ref('')
    const router = useRouter()
    const dateFormat = (unformedDate) => {
        return new Date(unformedDate).toLocaleDateString("ru-RU")
    }
    const displayedItems = () => {
        const start = (currentPage.value - 1) * itemsPerPage.value;
        const end = start + itemsPerPage.value;
        totalPages.value = Math.round(Math.round(clientsDataCopy.value.length) / itemsPerPage.value)
        arrData.value = clientsDataCopy.value.slice(start, end);
        router.replace({
            query: {
                ...router.currentRoute.value.query,
                sort: columnName.value,
                filter: inputValue.value,
                desc: ascendingOrder.value,
                elemPerPage: itemsPerPage.value,
                page: currentPage.value,
            }
        });
    }
    const searchTerm = (event) => {
        inputValue.value = event
        if (inputValue.value === '') {
            clientsDataCopy.value = clientsData
            selectPage(1)
            return
        }
        clientsDataCopy.value = clientsData.filter((item) => {
            return event.toLowerCase() === item.name.title.toLowerCase() ||
                event.toLowerCase() === item.name.first.toLowerCase() ||
                event.toLowerCase() === item.name.last.toLowerCase() ||
                event.toLowerCase() === item.gender.toLowerCase() ||
                event.toLowerCase() === item.location.city.toLowerCase() ||
                event.toLowerCase() === dateFormat(item.dob.date) ||
                event.toLowerCase() === item.email.toLowerCase() ||
                event.toLowerCase() === item.phone.toLowerCase()
        })
        selectPage(1)
    }
    const sortElements = (title, toggleClick = false) => {
        if (!toggleClick) {
            if (columnName.value !== title && columnName.value !== '') {
                ascendingOrder.value = 0
            } else {
                ascendingOrder.value = ascendingOrder.value < 2 ? ascendingOrder.value + 1 : 0
            }
        }
        columnName.value = title
        if (ascendingOrder.value === 0) {
            clientsDataCopySortElements.value = [...clientsDataCopy.value]
        }
        if (ascendingOrder.value === 2) {
            columnName.value = ''
            clientsDataCopy.value = clientsDataCopySortElements.value
        }
        if (title === 'fio') {
            if (ascendingOrder.value === 0) {
                clientsDataCopy.value = clientsDataCopy.value.sort((a, b) => {
                    return a.name.first.localeCompare(b.name.first);
                })
            }
            if (ascendingOrder.value === 1) {
                clientsDataCopy.value = clientsDataCopy.value.sort((a, b) => {
                    return b.name.first.localeCompare(a.name.first);
                })
            }
        }
        if (title === 'gender') {
            if (ascendingOrder.value === 0) {
                clientsDataCopy.value = clientsDataCopy.value.sort((a, b) => {
                    return a.gender.localeCompare(b.gender);
                })
            }
            if (ascendingOrder.value === 1) {
                clientsDataCopy.value = clientsDataCopy.value.sort((a, b) => {
                    return b.gender.localeCompare(a.gender);
                })
            }
        }
        if (title === 'location') {
            if (ascendingOrder.value === 0) {
                clientsDataCopy.value = clientsDataCopy.value.sort((a, b) => {
                    return a.location.city.localeCompare(b.location.city);
                })
            }
            if (ascendingOrder.value === 1) {
                clientsDataCopy.value = clientsDataCopy.value.sort((a, b) => {
                    return b.location.city.localeCompare(a.location.city);
                })
            }
        }
        if (title === 'dateBirth') {
            if (ascendingOrder.value === 0) {
                clientsDataCopy.value = clientsDataCopy.value.sort((a, b) => {
                    return a.dob.date.localeCompare(b.dob.date);
                })
            }
            if (ascendingOrder.value === 1) {
                clientsDataCopy.value = clientsDataCopy.value.sort((a, b) => {
                    return b.dob.date.localeCompare(a.dob.date);
                })
            }
        }
        if (title === 'email') {
            if (ascendingOrder.value === 0) {
                clientsDataCopy.value = clientsDataCopy.value.sort((a, b) => {
                    return a.email.localeCompare(b.email);
                })
            }
            if (ascendingOrder.value === 1) {
                clientsDataCopy.value = clientsDataCopy.value.sort((a, b) => {
                    return b.email.localeCompare(a.email);
                })
            }
        }
        if (title === 'phone') {
            if (ascendingOrder.value === 0) {
                clientsDataCopy.value = clientsDataCopy.value.sort((a, b) => {
                    return a.phone.localeCompare(b.phone);
                })
            }
            if (ascendingOrder.value === 1) {
                clientsDataCopy.value = clientsDataCopy.value.sort((a, b) => {
                    return b.phone.localeCompare(a.phone);
                })
            }
        }
        displayedItems()
    }
    const elementsPerPage = (event) => {
        itemsPerPage.value = parseInt(event)
        selectPage(1)
    }
    const prevPage = () => {
        currentPage.value--
        displayedItems()
    }
    const selectPage = (page) => {
        currentPage.value = page
        displayedItems()
    }
    const nextPage = () => {
        currentPage.value++
        displayedItems()
    }
    onMounted(() => {
        clientsDataCopy.value = clientsData
        if (router.currentRoute.value.query.desc !== undefined) {
            ascendingOrder.value = parseInt(router.currentRoute.value.query.desc)
            clientsDataCopySortElements.value = [...clientsDataCopy.value]
        }
        if (router.currentRoute.value.query.elemPerPage !== undefined) {
            itemsPerPage.value = parseInt(router.currentRoute.value.query.elemPerPage)
        }
        if (router.currentRoute.value.query.page !== undefined) {
            currentPage.value = parseInt(router.currentRoute.value.query.page)
        }
        if (router.currentRoute.value.query.sort !== undefined) {
            sortElements(router.currentRoute.value.query.sort, true)
        }
        if (router.currentRoute.value.query.filter !== undefined) {
            inputValue.value = router.currentRoute.value.query.filter
            searchTerm(inputValue.value)
        }
        displayedItems()
    })
</script>

<style lang="scss" scoped>
    .table-container {
        width: 100%;

        &__input {
            padding: 0;
            height: 20px;
        }

        &__select {
            height: 23px;
            margin-left: 10px;
        }

        &__controls {
            display: flex;
            align-items: center;
        }

        &__table {
            background-color: #B18460;
            width: 100%;
            border-collapse: collapse;
            margin-top: 20px;
        }

        &__th {
            cursor: pointer;
            background-color: #E3AE8B;
            transition: background-color 0.4s ease;
            padding: 10px;
            border: 1px solid #ccc;

            &:hover {
                background-color: #add8e6;
            }
        }

        &__td {
            padding: 10px;
            border: 1px solid #ccc;
        }

        &__avatar {
            width: 50px;
            height: 50px;
            border-radius: 50%;
        }
    }

    .pagination {
        margin-top: 20px;
        text-align: center;

        &__button {
            margin: 0 5px 5px 0;
        }
    }

    .select-page {
        border: 2px solid;
    }

    .header-content {
        display: flex;
        align-items: center;
        justify-content: center;
    }

    .header-content-svg {
        margin-left: 5px;
        width: 15px;
        height: 15px;
    }
</style>
