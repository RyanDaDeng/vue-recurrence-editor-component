<template>
    <div>
        <div class="input-group mb-3">
            <div class="input-group-prepend">
                <label class="input-group-text" for="repeat_option">Repeat</label>
            </div>
            <select class="custom-select" id="repeat_option" :value="value.repeatOption.type"
                    @change="updateRepeatOption($event)">
                <option value="every_week">every week</option>
                <option value="every_day">every day</option>
                <!--                <option value="every_week">on specific date(s)</option>-->
            </select>
        </div>


        <hr/>
        <div>
            <b> Repeat on</b>
        </div>
        <div>
            <div v-if="value.repeatOption.type === 'every_week'">
                <label v-for="date in weekDayCheckBox">
                    <input type="checkbox" :value="date.value" v-model="everyWeekPicker"
                           @change="updateWeekDayOption($event)">
                    <span>{{date.name}}</span>
                </label>
            </div>

            <div class="input-group mb-3">
                <div class="input-group-prepend">
                    <label class="input-group-text" for="at_time">At</label>
                </div>


                <input class="form-control" type="time" id="at_time" name="appt" :value="value.repeatAt" required
                       @change="updateRepeatAt($event)">
            </div>

            <!--            <hr/>-->
            <!--            <div>-->
            <!--                <b>Ends</b>-->
            <!--                <br/>-->

            <!--                <div>-->
            <!--                    <input type="radio" id="ends_never" value="ends_never" v-model="endsPicked"-->
            <!--                           @change="updateEndsPicked($event)">-->
            <!--                    <label for="ends_never">Never</label>-->
            <!--                </div>-->

            <!--                <div>-->
            <!--                    <input type="radio" id="ends_on" value="ends_on" v-model="endsPicked"-->
            <!--                           @change="updateEndsPicked($event)">-->
            <!--                    <label for="ends_on">On <input type="date" name="date" value="female"-->
            <!--                                                   :disabled="endsPicked !== 'ends_on'"></label>-->
            <!--                </div>-->

            <!--                <div>-->
            <!--                    <input type="radio" id="ends_after" value="ends_after" v-model="endsPicked"-->
            <!--                           @change="updateEndsPicked($event)">-->
            <!--                    <label for="ends_after">After <input type="number" min="1"-->
            <!--                                                         max="999"-->
            <!--                                                         :disabled="endsPicked !== 'ends_after'">-->
            <!--                        occurrences<br/></label>-->
            <!--                </div>-->

            <!--            </div>-->
        </div>
    </div>
</template>

<script>
    export default {
        name: 'RecurrenceEditor',
        props: ['value'],
        components: {},
        data() {
            return {
                _toString: '',
                everyWeekPicker: this.value.repeatOption.everyWeekPicker,
                endsPicked: this.value.endsPicked,
                weekDayCheckBox: [
                    {
                        name: 'Mon',
                        value: '1',
                        full_name: 'Monday'
                    },
                    {
                        name: 'Tue',
                        value: '2',
                        full_name: 'Tuesday'
                    },
                    {
                        name: 'Wed',
                        value: '3',
                        full_name: 'Wednesday'
                    },
                    {
                        name: 'Thu',
                        value: '4',
                        full_name: 'Thursday'
                    },
                    {
                        name: 'Fri',
                        value: '5',
                        full_name: 'Friday'
                    }
                    , {
                        name: 'Sat',
                        value: '6',
                        full_name: 'Saturday'
                    },
                    {
                        name: 'Sun',
                        value: '7',
                        full_name: 'Sunday'
                    },
                ]
            }
        },
        computed: {},
        methods: {
            updateWeekDayOption(event) {
                let data = {...this.value};
                let index = data.repeatOption.everyWeekPicker.indexOf(event.target.value);
                if (!event.target.checked) {
                    data.repeatOption.everyWeekPicker.splice(index, 1);
                }
                if (index === -1 && event.target.checked) {
                    data.repeatOption.everyWeekPicker.push(event.target.value);
                }
                data.repeatOption.everyWeekPicker.sort()
                this.$emit('input', data)
            },
            updateRepeatAt(event) {
                let data = {...this.value};
                data.repeatAt = event.target.value;
                this.$emit('input', data);
            },
            updateRepeatOption(event) {
                let data = {...this.value};

                switch (event.target.value) {
                    case 'every_week':
                        data.repeatOption = {
                            type: event.target.value,
                            everyWeekPicker: ['1', '2', '3', '4', '5']
                        };
                        this.everyWeekPicker = data.repeatOption.everyWeekPicker;
                        this.$emit('input', data);
                        break;
                    case 'every_day':
                        data.repeatOption = {
                            type: event.target.value,
                        };
                        this.$emit('input', data);
                        break;
                    default:
                        break;
                }
            },
            updateEndsPicked(event) {
                let data = {...this.value};
                data.endsPicked = event.target.value;
                this.$emit('input', data);
            },
        },
        created() {

        },
        mounted() {
        }
    }
</script>

<style scoped>

    input[type=checkbox] {
        display: none;
    }

    label :checked + span {
        background: #66bb6a;
        color: white;
    }

    label span {
        display: inline-block;
        background: lightgrey;
        height: 3em;
        width: 3em;
        line-height: 3em;
        text-align: center;
        border-radius: 50%;
        cursor: pointer;
        margin-right: 2px;
    }

    .round {
        position: relative;
    }

    .round label {
        background-color: #fff;
        border: 1px solid #ccc;
        border-radius: 50%;
        cursor: pointer;
        height: 28px;
        left: 0;
        position: absolute;
        top: 0;
        width: 28px;
    }


    .round input[type="checkbox"] {
        visibility: hidden;
    }

    .round input[type="checkbox"]:checked + label {
        background-color: #66bb6a;
        border-color: #66bb6a;
    }

    .round input[type="checkbox"]:checked + label:after {
        opacity: 1;
    }


</style>
