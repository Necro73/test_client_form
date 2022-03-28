<template>
    <div class="form">
        <div class="form-2">
            <div class="header-2">Инфо о клиенте</div>
            <div class="form-group" :class="{ 'form-group--error': $v.surname.$error }">
                <label class="form__label">Фамилия</label>
                <input class="form__input" v-model.trim="$v.surname.$model"/>
            </div>
            <div class="error" v-if="!$v.surname.required">*поле обязательно для заполнения</div>

            <div class="form-group" :class="{ 'form-group--error': $v.name.$error }">
                <label class="form__label">Имя</label>
                <input class="form__input" v-model.trim="$v.name.$model"/>
            </div>
            <div class="error" v-if="!$v.name.required">*поле обязательно для заполнения</div>

            <div class="form-group">
                <label class="form__label">Отчество</label>
                <input class="form__input" v-model.trim="$v.lastName.$model"/>
            </div>

            <div class="form-group" :class="{ 'form-group--error': $v.dateOfBirth.$error }">
                <label class="form__label">Дата рождения</label>
                <input class="form__input" v-model.trim="$v.dateOfBirth.$model"/>
            </div>
            <div class="error" v-if="!$v.dateOfBirth.required">*поле обязательно для заполнения</div>

            <div class="form-group" :class="{ 'form-group--error': $v.phone.$error }">
                <label class="form__label">Номер телефона</label>
                <input class="form__input" v-model.trim="$v.phone.$model"/>
            </div>
            <div class="error" v-if="!$v.phone.required">*поле обязательно для заполнения</div>
            <div class="error" v-if="!$v.phone.numeric">*поле принимает только цифры</div>
            <div class="error" v-if="!$v.phone.between">*поле должно быть длиной в 11 символов и начинаться на (7)
            </div>


            <div class="form-group" :class="{ 'form-group--error': $v.gender.$error }">
                <label class="form__label">Пол</label>
                <CustomSelector :options="genderValues" v-model="$v.gender.$model"/>
            </div>

            <div class="form-group" :class="{ 'form-group--error': $v.groupOfClients.$error }">
                <label class="form__label">Группа клиентов</label>
                <CustomSelector :options="groupOfClientsValue" v-model="$v.groupOfClients.$model" :multiple="true"/>
            </div>
            <div class="error" v-if="!$v.groupOfClients.selectorValidator">*должен быть выбран хотя бы один клиент</div>

            <div class="form-group" :class="{ 'form-group--error': $v.attendingDoctor.$error }">
                <label class="form__label">Лечащий врач</label>
                <CustomSelector :options="attendingDoctorValues" v-model="$v.attendingDoctor.$model"/>
            </div>

            <div class="form-group form-group-inline" :class="{ 'form-group--error': $v.noSMS.$error }">
                <label class="form__label form__label-inline">Не отправлять СМС</label>
                <input type="checkbox" class="form__input form-checkbox" v-model.trim="$v.noSMS.$model"/>
            </div>
        </div>

        <div class="form-2">
            <div class="header-2">Адрес</div>
            <div class="form-group" :class="{ 'form-group--error': $v.addressIndex.$error }">
                <label class="form__label">Индекс</label>
                <input class="form__input" v-model.trim="$v.addressIndex.$model"/>
            </div>
            <div class="form-group" :class="{ 'form-group--error': $v.addressCountry.$error }">
                <label class="form__label">Страна</label>
                <input class="form__input" v-model.trim="$v.addressCountry.$model"/>
            </div>
            <div class="form-group" :class="{ 'form-group--error': $v.addressRegion.$error }">
                <label class="form__label">Область</label>
                <input class="form__input" v-model.trim="$v.addressRegion.$model"/>
            </div>
            <div class="form-group" :class="{ 'form-group--error': $v.addressCity.$error }">
                <label class="form__label">Город</label>
                <input class="form__input" v-model.trim="$v.addressCity.$model"/>
            </div>
            <div class="error" v-if="!$v.groupOfClients.required">*поле обязательно для заполнения</div>
            <div class="form-group" :class="{ 'form-group--error': $v.addressStreet.$error }">
                <label class="form__label">Улица</label>
                <input class="form__input" v-model.trim="$v.addressStreet.$model"/>
            </div>
            <div class="form-group" :class="{ 'form-group--error': $v.addressHouse.$error }">
                <label class="form__label">Дом</label>
                <input class="form__input" v-model.trim="$v.addressHouse.$model"/>
            </div>
        </div>

        <div class="form-2">
            <div class="header-2">Паспорт</div>
            <div class="form-group" :class="{ 'form-group--error': $v.passportDocumentType.$error }">
                <label class="form__label">Тип документа</label>
                <CustomSelector :options="passportDocumentTypeValues" v-model="$v.passportDocumentType.$model"/>
            </div>
            <div class="form-group" :class="{ 'form-group--error': $v.passportRange.$error }">
                <label class="form__label">Серия</label>
                <input class="form__input" v-model.trim="$v.passportRange.$model"/>
            </div>
            <div class="form-group" :class="{ 'form-group--error': $v.passportNumber.$error }">
                <label class="form__label">Номер</label>
                <input class="form__input" v-model.trim="$v.passportNumber.$model"/>
            </div>
            <div class="form-group" :class="{ 'form-group--error': $v.passportIssuedBy.$error }">
                <label class="form__label">Кем выдан</label>
                <input class="form__input" v-model.trim="$v.passportIssuedBy.$model"/>
            </div>
            <div class="form-group" :class="{ 'form-group--error': $v.dateOfIssue.$error }">
                <label class="form__label">Дата выдачи</label>
                <input class="form__input" v-model.trim="$v.dateOfIssue.$model"/>
            </div>
            <div class="error" v-if="!$v.dateOfIssue.required">*поле обязательно для заполнения</div>
        </div>

        <div class="header-2" v-if="isClicked">Новый клиент успешно создан</div>
        <button class="button-complete" v-on:click="submitComplete()">Отправить форму</button>
    </div>
</template>

<script>
    import {required, between, numeric} from 'vuelidate/lib/validators'
    import CustomSelector from "@/components/CustomSelector";

    const contains = function(value)
    {
        return (value.length > 0);
    }

    export default {
        data() {
            return {
                surname: '',
                name: '',
                lastName: '',
                dateOfBirth: '',
                phone: '',
                gender: '',
                groupOfClients: [],
                attendingDoctor: '',
                noSMS: '',
                addressIndex: '',
                addressCountry: '',
                addressRegion: '',
                addressCity: '',
                addressStreet: '',
                addressHouse: '',
                passportDocumentType: '',
                passportRange: '',
                passportNumber: '',
                passportIssuedBy: '',
                dateOfIssue: '',

                attendingDoctorValues: ['Иванов', 'Захаров', 'Чернышева'],
                genderValues: ['Мужской', 'Женский'],
                passportDocumentTypeValues: ['Паспорт', 'Свидетельство о рождении', 'Вод. удостоверение'],
                groupOfClientsValue: ['VIP', 'Проблемные', 'ОМС'],

                isClicked: false,
            }
        },
        validations: {
            surname: {
                required,
            },
            name: {
                required,
            },
            lastName: {},
            dateOfBirth: {
                required,
            },
            phone: {
                required,
                numeric,
                between: between(70000000000, 79999999999),
            },
            gender: {},
            groupOfClients: {
                selectorValidator: contains
            },
            attendingDoctor: {},
            noSMS: {},
            addressIndex: {},
            addressCountry: {},
            addressRegion: {},
            addressCity: {
                required,
            },
            addressStreet: {},
            addressHouse: {},
            passportDocumentType: {
                required,
            },
            passportRange: {},
            passportNumber: {},
            passportIssuedBy: {},
            dateOfIssue: {
                required,
            },
        },
        name: "ClientForm",
        components: {
            CustomSelector
        },
        methods: {
            submitComplete() {
                this.$v.$touch();
                if (!this.$v.$invalid) {
                    console.log('Complete');
                    if (this.isClicked !== true) {
                        this.isClicked = true;
                    }
                } else {
                    console.log('Error');
                    if (this.isClicked !== false) {
                        this.isClicked = false;
                    }
                }
            }
        }
    }
</script>

<style lang="scss" scoped>
    .form {
        max-width: 500px;
        margin-left: auto;
        margin-right: auto;
        text-align: left;
    }

    .form-group {
        margin-bottom: 2rem;
    }

    .form-group-inline {
        display: flex;
        align-items: center;
    }

    .form__label {
        font-size: .8125rem;
        color: #4b6372;
        margin-bottom: 0.3125rem;
        margin-left: 0.875rem;
        display: block;
        font-family: "Lato", sans-serif;
    }

    .form__label-inline {
        margin-bottom: 0;
        padding-top: 4px;
    }

    .form__input, .form__textarea {
        font-family: "Lato", sans-serif;
        font-size: .875rem;
        font-weight: 300;
        color: #374853;
        line-height: 2.375rem;
        min-height: 2.375rem;
        position: relative;
        border: 1px solid #E8E8E8;
        border-radius: 5px;
        background: #fff;
        padding: 0 0.8125rem;
        width: 100%;
        transition: border .1s ease;
        box-sizing: border-box;
    }

    .form-group .form__input, .form-group .form__textarea {
        margin-bottom: 0;
    }

    .form-group__message, .error {
        font-size: .75rem;
        line-height: 1;
        display: none;
        margin-left: 14px;
        margin-top: -1.6875rem;
        margin-bottom: 0.9375rem;
    }

    .form-group--error + .form-group__message, .form-group--error + .error {
        display: block;
        color: #f57f6c;
    }

    .header-2 {
        padding-bottom: 2rem;
        font-size: 1.25rem;
    }

    .form-2 {
        background-color: #f4f4f4;
        padding: 1.25em;
        border-radius: 5px;
        margin-bottom: 5px;
    }

    .form-checkbox {
        width: 20px;
        height: 20px;
        margin-left: 8px;
    }

    .button-complete {
        position: relative;
        background-color: #4CAF50;
        border: none;
        font-size: 28px;
        color: #FFFFFF;
        padding: 20px;
        width: 100%;
        border-radius: 5px;
        text-align: center;
        transition-duration: 0.4s;
        text-decoration: none;
        overflow: hidden;
        cursor: pointer;
    }
    .button-complete:after {
        content: "";
        background: #f1f1f1;
        display: block;
        position: absolute;
        padding-top: 300%;
        padding-left: 350%;
        margin-left: -20px !important;
        margin-top: -120%;
        opacity: 0;
        transition: all 0.8s;
    }
    .button-complete:active:after {
        padding: 0;
        margin: 0;
        opacity: 1;
        transition: 0s
    }
</style>