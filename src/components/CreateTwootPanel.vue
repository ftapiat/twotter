<template>
    <form @submit.prevent="createNewTwoot">
        <label for="newToot"><strong>New Twoot</strong></label><br>
        <textarea id="newToot" rows="4" v-model="state.newTwootContent"></textarea>
        <br>

        <div>
            <label for="newTootType"><strong>Type: </strong></label>
            <select name="" id="newTootType" v-model="state.selectedTwootType">
                <option :value="option.value"
                        v-for="(option, index) in state.twootTypes"
                        :key="index"
                >
                    {{ option.name }}
                </option>
            </select>
        </div>

        <button>
            Twoot!
        </button>

    </form>
</template>

<script>
    import { reactive, computed } from 'vue'; // Composition API

    export default {
        name: "CreateTwootPanel",
        setup(props, context) {
            const state = reactive({ // Data
                newTwootContent: '',
                selectedTwootType: 'instant',

                twootTypes: [
                    {value: 'draft', name: 'Draft'},
                    {value: 'instant', name: 'Instant Twoot'},
                ],
                isLoading: false,
                followers: 0,
                user: {
                    id: 1,
                    username: '_dddd',
                    firstName: 'Francisco',
                    lastName: 'Tapia',
                    email: 'test@test.com',
                    isAdmin: true,
                    twoots: [
                        {id: 1, content: 'Twotter is Amazing!'},
                        {id: 2, content: "Don't forget to Subscribe"},
                    ],
                }
            });

            const newTwootCharactedCount = computed( () => state.newTwootContent.length); // Computed

            function createNewTwoot() { // Methods
                if (state.newTwootContent && state.selectedTwootType !== 'draft'){
                    context.emit('add-twoot', state.newTwootContent);
                    state.newTwootContent = '';
                }
            }

            return {
                state,
                newTwootCharactedCount,
                createNewTwoot,
            };
        },
    }
</script>