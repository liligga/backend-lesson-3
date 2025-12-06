<script setup lang="ts">
import { ref, computed } from 'vue'

type Choice = { id: number; text: string; correct?: boolean }
type Question = { id: number; text: string; choices: Choice[] }

const questions = ref<Question[]>([
    {
    id: 1,
    text: 'Что такое инкапсуляция в Python?',
    choices: [
        { id: 1, text: 'Создание новых классов из существующих' },
        { id: 2, text: 'Механизм объединения данных и методов в объект и сокрытие деталей реализации', correct: true },
        { id: 3, text: 'Возможность использовать один интерфейс для разных типов объектов' },
        { id: 4, text: 'Создание шаблонов для других классов' },
    ],
    },
    {
    id: 2,
    text: 'Как обозначается приватный атрибут в Python?',
    choices: [
        { id: 1, text: 'С одним подчёркиванием в начале (_атрибут)' },
        { id: 2, text: 'С двумя подчёркиваниями в начале (__атрибут)', correct: true },
        { id: 3, text: 'С ключевым словом private' },
        { id: 4, text: 'С символом @ перед именем' },
    ],
    },
    {
    id: 3,
    text: 'Для чего используется декоратор @property?',
    choices: [
        { id: 1, text: 'Для создания абстрактных методов' },
        { id: 2, text: 'Для создания статических методов' },
        { id: 3, text: 'Для предоставления доступа к приватным атрибутам через методы', correct: true },
        { id: 4, text: 'Для наследования от родительского класса' },
    ],
    },
    {
    id: 4,
    text: 'Что такое наследование в ООП?',
    choices: [
        { id: 1, text: 'Копирование кода из одного файла в другой' },
        { id: 2, text: 'Механизм создания нового класса на основе существующего', correct: true },
        { id: 3, text: 'Способ защиты данных от изменения' },
        { id: 4, text: 'Автоматическое удаление неиспользуемых методов' },
    ],
    },
    {
    id: 5,
    text: 'Что такое абстракция в ООП?',
    choices: [
        { id: 1, text: 'Защита данных от неправильного доступа' },
        { id: 2, text: 'Создание копий объектов' },
        { id: 3, text: 'Принцип, позволяющий скрывать сложные детали реализации, предоставляя только необходимый функционал', correct: true },
        { id: 4, text: 'Возможность создавать новые классы на основе существующих' },
    ]
    },
    {
    id: 6,
    text: 'В чём разница между защищённым (_) и приватным (__) атрибутом?',
    choices: [
        { id: 1, text: 'Никакой разницы нет, это одно и то же' },
        { id: 2, text: 'Приватный атрибут недоступен вообще, защищённый доступен везде' },
        { id: 3, text: 'К защищённому не рекомендуется обращаться извне, приватный искажается через name mangling', correct: true },
        { id: 4, text: 'Защищённый используется только в дочерних классах' },
    ]
    },
    {
    id: 7,
    text: 'Можно ли создать экземпляр абстрактного класса?',
    choices: [
        { id: 1, text: 'Да, абстрактные классы ничем не отличаются от обычных' },
        { id: 2, text: 'Нет, абстрактный класс служит шаблоном и не может иметь экземпляров', correct: true },
        { id: 3, text: 'Да, но только если определены все методы' },
        { id: 4, text: 'Да, но только внутри дочерних классов' },
    ],
    },
    {
    id: 8,
    text: 'Какое ключевое слово используется для вызова методов родительского класса?',
    choices: [
        { id: 1, text: 'parent()' },
        { id: 2, text: 'base()' },
        { id: 3, text: 'super()', correct: true },
        { id: 4, text: 'inherit()' },
    ],
    },
    {
    id: 9,
    text: 'Что произойдёт, если дочерний класс определяет метод с таким же именем, как у родителя?',
    choices: [
        { id: 1, text: 'Будет ошибка, нельзя переопределять методы' },
        { id: 2, text: 'Метод дочернего класса переопределит (override) метод родителя', correct: true },
        { id: 3, text: 'Оба метода будут вызываться одновременно' },
        { id: 4, text: 'Метод родителя удалится из памяти' },
    ],
    },
    {
    id: 10,
    text: 'Что такое полиморфизм в ООП?',
    choices: [
        { id: 1, text: 'Создание множества классов с одинаковыми именами' },
        { id: 2, text: 'Возможность использовать один интерфейс для разных типов объектов', correct: true },
        { id: 3, text: 'Сокрытие внутренней реализации класса' },
        { id: 4, text: 'Создание приватных атрибутов' },
    ],
    },
    {
    id: 11,
    text: 'Зачем нужна инкапсуляция при работе с атрибутами класса?',
    choices: [
        { id: 1, text: 'Чтобы ускорить выполнение программы' },
        { id: 2, text: 'Для защиты данных от неправильного доступа и валидации при изменении', correct: true },
        { id: 3, text: 'Чтобы код занимал меньше места в памяти' },
        { id: 4, text: 'Для автоматического создания документации' },
    ]
    },
    {
    id: 12,
    text: 'Какой код правильно использует @property для доступа к приватному атрибуту?',
    choices: [
        { id: 1, text: '@property\ndef __speed(self): return self.__speed' },
        { id: 2, text: 'property\ndef speed(self): return self.__speed' },
        { id: 3, text: '@property\ndef speed(self): return self.__speed', correct: true },
        { id: 4, text: '@getter\ndef speed(self): return self.speed' },
    ]
    }
])

const currentIndex = ref(0)
const selected = ref<number | null>(null)
const answers = ref<{ questionId: number; selectedId: number }[]>([])
const showResults = ref(false)

// Results pagination
const pageSize = 3
const resultsPage = ref(0)
const totalPages = computed(() => Math.ceil(questions.value.length / pageSize))
const pagedQuestions = computed(() => {
    const start = resultsPage.value * pageSize
    return questions.value.slice(start, start + pageSize)
})

function prevPage() {
    if (resultsPage.value > 0) resultsPage.value -= 1
}
function nextPage() {
    if (resultsPage.value < totalPages.value - 1) resultsPage.value += 1
}

const currentQuestion = computed(() => questions.value[currentIndex.value])

function submitAnswer() {
    if (selected.value == null) return
    answers.value.push({
    questionId: currentQuestion.value.id,
    selectedId: selected.value,
    })
    selected.value = null
    if (currentIndex.value < questions.value.length - 1) {
    currentIndex.value += 1
    } else {
    showResults.value = true
    }
}

function isChoiceCorrect(q: Question, choiceId: number) {
    return !!q.choices.find(c => c.id === choiceId)?.correct
}

function userSelectedFor(questionId: number) {
    return answers.value.find(a => a.questionId === questionId)?.selectedId ?? null
}
</script>

<template>
    <div w="full" max-w="800px" m="auto" p="3" border="~ main rounded-md" bg="white dark:gray-900" text="sm">
    <template v-if="!showResults">
        <h3 text="base" font="semibold">Викторина по ООП • Основы Python</h3>
        <div mb="3" flex="~ justify-between items-center">
        <h4 text="base" font="semibold">Вопрос {{ currentIndex + 1 }} из {{ questions.length }}</h4>
        </div>
        <div mb="3" text="sm md:base">{{ currentQuestion.text }}</div>

        <div grid="~ cols-1 gap-2 md:cols-2" mb="4">
        <label
            v-for="choice in currentQuestion.choices"
            :key="choice.id"
            border="~ main rounded-md"
            p="2"
            flex="~ items-center gap-3"
            hover:bg="gray-400 opacity-10"
        >
            <input
            type="radio"
            name="choice"
            :value="choice.id"
            v-model="selected"
            />
            <span>{{ choice.text }}</span>
        </label>
        </div>

        <div flex="~ justify-between items-center">
        <div text="xs gray-500">Викторина по ООП • Основы Python</div>
        <button
            :disabled="selected == null"
            :aria-disabled="selected == null"
            p="2"
            px="3"
            border="~ main rounded-md"
            bg="blue-600 disabled:gray-300"
            text="white disabled:gray-600 xs"
            @click="submitAnswer"
        >
            {{ currentIndex + 1 === questions.length ? 'Завершить' : 'Далее' }}
        </button>
        </div>
    </template>

    <template v-else>
        <h2 text="base" font="bold" mb="3">Результаты</h2>
        <div mb="2" text="xs gray-600">Зелёная галочка означает, что вы ответили правильно.</div>
        <div overflow="auto">
        <table w="full" border="~ main rounded-md" text="xs" class="results-table">
            <thead bg="gray-100 dark:gray-800" text="xs">
            <tr>
                <th p="2" text="left">#</th>
                <th p="2" text="left">Вопрос</th>
                <th p="2" text="left">Ваш ответ</th>
                <th p="2" text="left">Правильный ответ</th>
            </tr>
            </thead>
            <tbody>
            <tr v-for="q in pagedQuestions" :key="q.id" hover:bg="gray-400 opacity-10">
                <td p="2">{{ q.id }}</td>
                <td p="2">{{ q.text }}</td>
                <td p="2" flex="~ items-center gap-2">
                <span>{{ q.choices.find(c => c.id === userSelectedFor(q.id))?.text || '—' }}</span>
                <span v-if="isChoiceCorrect(q, userSelectedFor(q.id) as number)" text="green-600">✔</span>
                </td>
                <td p="2">{{ q.choices.find(c => c.correct)?.text }}</td>
            </tr>
            </tbody>
        </table>
        </div>

        <div mt="3" flex="~ justify-between items-center">
        <button
            p="2"
            px="3"
            border="~ main rounded-md"
            :disabled="resultsPage === 0"
            :aria-disabled="resultsPage === 0"
            @click="prevPage"
        >
            ←
        </button>
        <div text="xs gray-500">Страница {{ resultsPage + 1 }} из {{ totalPages }}</div>
        <button
            p="2"
            px="3"
            border="~ main rounded-md"
            :disabled="resultsPage >= totalPages - 1"
            :aria-disabled="resultsPage >= totalPages - 1"
            @click="nextPage"
        >
            →
        </button>
        </div>
    </template>
    </div>
</template>
