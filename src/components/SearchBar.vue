<template>
    <nav class="navbar navbar-light bg-light">
        <div class="container-fluid">
            <!-- 
                v-model binds the input value to the data property searchQuery
                @click calls the method searchMovies when the button is clicked
            -->
            <input v-model="searchQuery" class="form-control me-2" type="search" placeholder="Search" aria-label="Search">
            <button @click="searchMovies" class="btn btn-outline-success" type="button">Search</button>
        </div>
    </nav>

    <div class="movie-info">
        <h2>Movie Information:</h2>
        <ul>
            <!-- 
                v-for iterates over the movies array and displays the movie information
                :key is used to give each movie a unique identifier
            -->
            <li v-for="movie in movies" :key="movie.id">
                <!-- Copied .title, .orginal_title, .original_language, .vote_average from the API code, visualized using Postman -->
                <h3>{{ movie.title }}</h3>
                <p>Original Title: {{ movie.original_title }}</p>
                <p>Language: {{ movie.original_language }}
                    <Icon :icon="getFlagIcon(movie.original_language)" style="font-size: 24px;" />
                    <Icon icon="flag-icon flag-icon-gb"/>
                </p>
                <p>Rating: {{ movie.vote_average }}</p>
            </li>
        </ul>
    </div>
</template>


<script>
import { store } from '../store.js'
import { Icon } from '@iconify/vue';

export default {
    name: 'SearchBar',

    components: {
        Icon,
    },

    created() {
        this.searchMovies();
    },

    data() {

        return {
            store,

            // Adding icons
            icons: {
                'en': 'flag-icon flag-icon-gb',
                'es': 'flag-icon flag-icon-es',
                'fr': 'flag-icon flag-icon-fr',
                'it': 'flag-icon flag-icon-it',
                'ja': 'flag-icon flag-icon-jp',
                'ko': 'flag-icon flag-icon-kr',
                'pt': 'flag-icon flag-icon-pt',
                'ru': 'flag-icon flag-icon-ru',
                'zh': 'flag-icon flag-icon-cn',
                'de': 'flag-icon flag-icon-de',
                'nl': 'flag-icon flag-icon-nl',
                'sv': 'flag-icon flag-icon-se',
                'no': 'flag-icon flag-icon-no',
                'fi': 'flag-icon flag-icon-fi',
                'da': 'flag-icon flag-icon-dk',
                'hi': 'flag-icon flag-icon-in',
                'ar': 'flag-icon flag-icon-sa',
            },

            // Adding searchQuery and movies to the data object
            searchQuery: '',
            countryList: [
                { name: "Afghanistan", code: "AF", languages: "Persian", flag: "flag-icon flag-icon-af" },
                { name: "Aland Islands", code: "AX", languages: "Swedish", flag: "flag-icon flag-icon-ax" },
                { name: "Albania", code: "AL", languages: "Albanian", flag: "flag-icon flag-icon-al" },
                { name: "Algeria", code: "DZ", languages: "Arabic", flag: "flag-icon flag-icon-dz" },
                { name: "American Samoa", code: "AS", languages: "English", flag: "flag-icon flag-icon-as" },
                { name: "Andorra", code: "AD", languages: "Catalan", flag: "flag-icon flag-icon-ad" },
                { name: "Angola", code: "AO", languages: "Portuguese", flag: "flag-icon flag-icon-ao" },
                { name: "Anguilla", code: "AI", languages: "English", flag: "flag-icon flag-icon-ai" },
                { name: "Antigua and Barbuda", code: "AG", languages: "English", flag: "flag-icon flag-icon-ag" },
                { name: "Argentina", code: "AR", languages: "Spanish", flag: "flag-icon flag-icon-ar" },
                { name: "Armenia", code: "AM", languages: "Armenian", flag: "flag-icon flag-icon-am" },
                { name: "Aruba", code: "AW", languages: "Dutch", flag: "flag-icon flag-icon-aw" },
                { name: "Australia", code: "AU", languages: "English", flag: "flag-icon flag-icon-au" },
                { name: "Austria", code: "AT", languages: "German", flag: "flag-icon flag-icon-at" },
                { name: "Azerbaijan", code: "AZ", languages: "Azerbaijani", flag: "flag-icon flag-icon-az" },
                { name: "Bahamas", code: "BS", languages: "English", flag: "flag-icon flag-icon-bs" },
                { name: "Bahrain", code: "BH", languages: "Arabic", flag: "flag-icon flag-icon-bh" },
                { name: "Bangladesh", code: "BD", languages: "Bengali", flag: "flag-icon flag-icon-bd" },
                { name: "Barbados", code: "BB", languages: "English", flag: "flag-icon flag-icon-bb" },
                { name: "Belarus", code: "BY", languages: "Belarusian", flag: "flag-icon flag-icon-by" },
                { name: "Belgium", code: "BE", languages: "Dutch, French, German", flag: "flag-icon flag-icon-be" },
                { name: "Belize", code: "BZ", languages: "English", flag: "flag-icon flag-icon-bz" },
                { name: "Benin", code: "BJ", languages: "French", flag: "flag-icon flag-icon-bj" },
                { name: "Bermuda", code: "BM", languages: "English", flag: "flag-icon flag-icon-bm" },
                { name: "Bhutan", code: "BT", languages: "Dzongkha", flag: "flag-icon flag-icon-bt" },
                { name: "Bolivia", code: "BO", languages: "Spanish", flag: "flag-icon flag-icon-bo" },
                { name: "Bonaire, Sint Eustatius and Saba", code: "BQ", languages: "Dutch", flag: "flag-icon flag-icon-bq" },
                { name: "Bosnia and Herzegovina", code: "BA", languages: "Bosnian, Croatian, Serbian", flag: "flag-icon flag-icon-ba" },
                { name: "Botswana", code: "BW", languages: "Setswana, English", flag: "flag-icon flag-icon-bw" },
                { name: "Bouvet Island", code: "BV", languages: "Uninhabited", flag: "flag-icon flag-icon-bv" },
                { name: "Brazil", code: "BR", languages: "Portuguese", flag: "flag-icon flag-icon-br" },
                { name: "British Indian Ocean Territory", code: "IO", languages: "English", flag: "flag-icon flag-icon-io" },
                { name: "Brunei Darussalam", code: "BN", languages: "Malay", flag: "flag-icon flag-icon-bn" },
                { name: "Bulgaria", code: "BG", languages: "Bulgarian", flag: "flag-icon flag-icon-bg" },
                { name: "Burkina Faso", code: "BF", languages: "French", flag: "flag-icon flag-icon-bf" },
                { name: "Burundi", code: "BI", languages: "Kirundi, French", flag: "flag-icon flag-icon-bi" },
                { name: "Cambodia", code: "KH", languages: "Khmer", flag: "flag-icon flag-icon-kh" },
                { name: "Cameroon", code: "CM", languages: "English, French", flag: "flag-icon flag-icon-cm" },
                { name: "Canada", code: "CA", languages: "English, French", flag: "flag-icon flag-icon-ca" },
                { name: "Cape Verde", code: "CV", languages: "Portuguese", flag: "flag-icon flag-icon-cv" },
                { name: "Cayman Islands", code: "KY", languages: "English", flag: "flag-icon flag-icon-ky" },
                { name: "Central African Republic", code: "CF", languages: "French, Sango", flag: "flag-icon flag-icon-cf" },
                { name: "Chad", code: "TD", languages: "French, Arabic", flag: "flag-icon flag-icon-td" },
                { name: "Chile", code: "CL", languages: "Spanish", flag: "flag-icon flag-icon-cl" },
                { name: "China", code: "CN", languages: "Chinese", flag: "flag-icon flag-icon-cn" },
                { name: "Christmas Island", code: "CX", languages: "English", flag: "flag-icon flag-icon-cx" },
                { name: "Cocos (Keeling) Islands", code: "CC", languages: "English", flag: "flag-icon flag-icon-cc" },
                { name: "Colombia", code: "CO", languages: "Spanish", flag: "flag-icon flag-icon-co" },
                { name: "Comoros", code: "KM", languages: "Arabic, French, Comorian", flag: "flag-icon flag-icon-km" },
                { name: "Congo", code: "CG", languages: "French", flag: "flag-icon flag-icon-cg" },
                { name: "Congo, Democratic Republic of the Congo", code: "CD", languages: "French", flag: "flag-icon flag-icon-cd" },
                { name: "Cook Islands", code: "CK", languages: "English, Cook Islands Maori", flag: "flag-icon flag-icon-ck" },
                { name: "Costa Rica", code: "CR", languages: "Spanish", flag: "flag-icon flag-icon-cr" },
                { name: "Cote D'Ivoire", code: "CI", languages: "French", flag: "flag-icon flag-icon-ci" },
                { name: "Croatia", code: "HR", languages: "Croatian", flag: "flag-icon flag-icon-hr" },
                { name: "Cuba", code: "CU", languages: "Spanish", flag: "flag-icon flag-icon-cu" },
                { name: "Curacao", code: "CW", languages: "Dutch, Papiamento", flag: "flag-icon flag-icon-cw" },
                { name: "Cyprus", code: "CY", languages: "Greek, Turkish", flag: "flag-icon flag-icon-cy" },
                { name: "Czech Republic", code: "CZ", languages: "Czech", flag: "flag-icon flag-icon-cz" },
                { name: "Denmark", code: "DK", languages: "Danish", flag: "flag-icon flag-icon-dk" },
                { name: "Djibouti", code: "DJ", languages: "French, Arabic", flag: "flag-icon flag-icon-dj" },
                { name: "Dominica", code: "DM", languages: "English", flag: "flag-icon flag-icon-dm" },
                { name: "Dominican Republic", code: "DO", languages: "Spanish", flag: "flag-icon flag-icon-do" },
                { name: "Ecuador", code: "EC", languages: "Spanish", flag: "flag-icon flag-icon-ec" },
                { name: "Egypt", code: "EG", languages: "Arabic", flag: "flag-icon flag-icon-eg" },
                { name: "El Salvador", code: "SV", languages: "Spanish", flag: "flag-icon flag-icon-sv" },
                { name: "Equatorial Guinea", code: "GQ", languages: "Spanish, French, Portuguese", flag: "flag-icon flag-icon-gq" },
                { name: "Eritrea", code: "ER", languages: "Tigrinya, Arabic, English", flag: "flag-icon flag-icon-er" },
                { name: "Estonia", code: "EE", languages: "Estonian", flag: "flag-icon flag-icon-ee" },
                { name: "Ethiopia", code: "ET", languages: "Amharic", flag: "flag-icon flag-icon-et" },
                { name: "Falkland Islands (Malvinas)", code: "FK", languages: "English", flag: "flag-icon flag-icon-fk" },
                { name: "Faroe Islands", code: "FO", languages: "Faroese, Danish", flag: "flag-icon flag-icon-fo" },
                { name: "Fiji", code: "FJ", languages: "English, Fijian", flag: "flag-icon flag-icon-fj" },
                { name: "Finland", code: "FI", languages: "Finnish, Swedish", flag: "flag-icon flag-icon-fi" },
                { name: "France", code: "FR", languages: "French", flag: "flag-icon flag-icon-fr" },
                { name: "French Guiana", code: "GF", languages: "French", flag: "flag-icon flag-icon-gf" },
                { name: "French Polynesia", code: "PF", languages: "French", flag: "flag-icon flag-icon-pf" },
                { name: "French Southern Territories", code: "TF", languages: "French", flag: "flag-icon flag-icon-tf" },
                { name: "Gabon", code: "GA", languages: "French", flag: "flag-icon flag-icon-ga" },
                { name: "Gambia", code: "GM", languages: "English", flag: "flag-icon flag-icon-gm" },
                { name: "Georgia", code: "GE", languages: "Georgian", flag: "flag-icon flag-icon-ge" },
                { name: "Germany", code: "DE", languages: "German", flag: "flag-icon flag-icon-de" },
                { name: "Ghana", code: "GH", languages: "English", flag: "flag-icon flag-icon-gh" },
                { name: "Gibraltar", code: "GI", languages: "English", flag: "flag-icon flag-icon-gi" },
                { name: "Greece", code: "GR", languages: "Greek", flag: "flag-icon flag-icon-gr" },
                { name: "Greenland", code: "GL", languages: "Greenlandic, Danish", flag: "flag-icon flag-icon-gl" },
                { name: "Grenada", code: "GD", languages: "English", flag: "flag-icon flag-icon-gd" },
                { name: "Guadeloupe", code: "GP", languages: "French", flag: "flag-icon flag-icon-gp" },
                { name: "Guam", code: "GU", languages: "English, Chamorro", flag: "flag-icon flag-icon-gu" },
                { name: "Guatemala", code: "GT", languages: "Spanish", flag: "flag-icon flag-icon-gt" },
                { name: "Guernsey", code: "GG", languages: "English", flag: "flag-icon flag-icon-gg" },
                { name: "Guinea", code: "GN", languages: "French", flag: "flag-icon flag-icon-gn" },
                { name: "Guinea-Bissau", code: "GW", languages: "Portuguese", flag: "flag-icon flag-icon-gw" },
                { name: "Guyana", code: "GY", languages: "English", flag: "flag-icon flag-icon-gy" },
                { name: "Haiti", code: "HT", languages: "French, Haitian Creole", flag: "flag-icon flag-icon-ht" },
                { name: "Heard Island and McDonald Islands", code: "HM", languages: "English", flag: "flag-icon flag-icon-hm" },
                { name: "Holy See (Vatican City State)", code: "VA", languages: "Latin, Italian", flag: "flag-icon flag-icon-va" },
                { name: "Honduras", code: "HN", languages: "Spanish", flag: "flag-icon flag-icon-hn" },
                { name: "Hong Kong", code: "HK", languages: "Chinese, English", flag: "flag-icon flag-icon-hk" },
                { name: "Hungary", code: "HU", languages: "Hungarian", flag: "flag-icon flag-icon-hu" },
                { name: "Iceland", code: "IS", languages: "Icelandic", flag: "flag-icon flag-icon-is" },
                { name: "India", code: "IN", languages: "Hindi, English", flag: "flag-icon flag-icon-in" },
                { name: "Indonesia", code: "ID", languages: "Indonesian", flag: "flag-icon flag-icon-id" },
                { name: "Iran, Islamic Republic of", code: "IR", languages: "Persian", flag: "flag-icon flag-icon-ir" },
                { name: "Iraq", code: "IQ", languages: "Arabic, Kurdish", flag: "flag-icon flag-icon-iq" },
                { name: "Ireland", code: "IE", languages: "Irish, English", flag: "flag-icon flag-icon-ie" },
                { name: "Isle of Man", code: "IM", languages: "English, Manx", flag: "flag-icon flag-icon-im" },
                { name: "Israel", code: "IL", languages: "Hebrew, Arabic", flag: "flag-icon flag-icon-il" },
                { name: "Italy", code: "IT", languages: "Italian", flag: "flag-icon flag-icon-it" },
                { name: "Jamaica", code: "JM", languages: "English", flag: "flag-icon flag-icon-jm" },
                { name: "Japan", code: "JP", languages: "Japanese", flag: "flag-icon flag-icon-jp" },
                { name: "Jersey", code: "JE", languages: "English", flag: "flag-icon flag-icon-je" },
                { name: "Jordan", code: "JO", languages: "Arabic", flag: "flag-icon flag-icon-jo" },
                { name: "Kazakhstan", code: "KZ", languages: "Kazakh, Russian", flag: "flag-icon flag-icon-kz" },
                { name: "Kenya", code: "KE", languages: "Swahili, English", flag: "flag-icon flag-icon-ke" },
                { name: "Kiribati", code: "KI", languages: "English, Kiribati", flag: "flag-icon flag-icon-ki" },
                { name: "Korea, Democratic People's Republic of", code: "KP", languages: "Korean", flag: "flag-icon flag-icon-kp" },
                { name: "Korea, Republic of", code: "KR", languages: "Korean", flag: "flag-icon flag-icon-kr" },
                { name: "Kuwait", code: "KW", languages: "Arabic", flag: "flag-icon flag-icon-kw" },
                { name: "Kyrgyzstan", code: "KG", languages: "Kyrgyz, Russian", flag: "flag-icon flag-icon-kg" },
                { name: "Lao People's Democratic Republic", code: "LA", languages: "Lao", flag: "flag-icon flag-icon-la" },
                { name: "Latvia", code: "LV", languages: "Latvian", flag: "flag-icon flag-icon-lv" },
                { name: "Lebanon", code: "LB", languages: "Arabic", flag: "flag-icon flag-icon-lb" },
                { name: "Lesotho", code: "LS", languages: "English, Sesotho", flag: "flag-icon flag-icon-ls" },
                { name: "Liberia", code: "LR", languages: "English", flag: "flag-icon flag-icon-lr" },
                { name: "Libya", code: "LY", languages: "Arabic", flag: "flag-icon flag-icon-gl" },
                { name: "Liechtenstein", code: "LI", languages: "German", flag: "flag-icon flag-icon-li" },
                { name: "Lithuania", code: "LT", languages: "Lithuanian", flag: "flag-icon flag-icon-lt" },
                { name: "Luxembourg", code: "LU", languages: "Luxembourgish, French, German", flag: "flag-icon flag-icon-lu" },
                { name: "Macao", code: "MO", languages: "Chinese, Portuguese", flag: "flag-icon flag-icon-mo" },
                { name: "Macedonia, the former Yugoslav Republic of", code: "MK", languages: "Macedonian", flag: "flag-icon flag-icon-mk" },
                { name: "Madagascar", code: "MG", languages: "Malagasy, French", flag: "flag-icon flag-icon-mg" },
                { name: "Malawi", code: "MW", languages: "English, Chichewa", flag: "flag-icon flag-icon-mw" },
                { name: "Malaysia", code: "MY", languages: "Malay", flag: "flag-icon flag-icon-my" },
                { name: "Maldives", code: "MV", languages: "Dhivehi", flag: "flag-icon flag-icon-mv" },
                { name: "Mali", code: "ML", languages: "French", flag: "flag-icon flag-icon-ml" },
                { name: "Malta", code: "MT", languages: "Maltese, English", flag: "flag-icon flag-icon-mt" },
                { name: "Marshall Islands", code: "MH", languages: "English, Marshallese", flag: "flag-icon flag-icon-mh" },
                { name: "Martinique", code: "MQ", languages: "French", flag: "flag-icon flag-icon-mq" },
                { name: "Mauritania", code: "MR", languages: "Arabic", flag: "flag-icon flag-icon-mr" },
                { name: "Mauritius", code: "MU", languages: "English", flag: "flag-icon flag-icon-mu" },
                { name: "Mayotte", code: "YT", languages: "French", flag: "flag-icon flag-icon-yt" },
                { name: "Mexico", code: "MX", languages: "Spanish", flag: "flag-icon flag-icon-mx" },
                { name: "Micronesia, Federated States of", code: "FM", languages: "English", flag: "flag-icon flag-icon-fm" },
                { name: "Moldova, Republic of", code: "MD", languages: "Moldavian", flag: "flag-icon flag-icon-md" },
                { name: "Monaco", code: "MC", languages: "French", flag: "flag-icon flag-icon-mc" },
                { name: "Mongolia", code: "MN", languages: "Mongolian", flag: "flag-icon flag-icon-mn" },
                { name: "Montenegro", code: "ME", languages: "Serbian, Montenegrin", flag: "flag-icon flag-icon-me" },
                { name: "Montserrat", code: "MS", languages: "English", flag: "flag-icon flag-icon-ms" },
                { name: "Morocco", code: "MA", languages: "Arabic", flag: "flag-icon flag-icon-ma" },
                { name: "Mozambique", code: "MZ", languages: "Portuguese", flag: "flag-icon flag-icon-mz" },
                { name: "Myanmar", code: "MM", languages: "Burmese", flag: "flag-icon flag-icon-mm" },
                { name: "Namibia", code: "NA", languages: "English", flag: "flag-icon flag-icon-na" },
                { name: "Nauru", code: "NR", languages: "Nauruan, English", flag: "flag-icon flag-icon-nr" },
                { name: "Nepal", code: "NP", languages: "Nepali", flag: "flag-icon flag-icon-np" },
                { name: "Netherlands", code: "NL", languages: "Dutch", flag: "flag-icon flag-icon-nl" },
                { name: "New Caledonia", code: "NC", languages: "French", flag: "flag-icon flag-icon-nc" },
                { name: "New Zealand", code: "NZ", languages: "English, Maori", flag: "flag-icon flag-icon-nz" },
                { name: "Nicaragua", code: "NI", languages: "Spanish", flag: "flag-icon flag-icon-ni" },
                { name: "Niger", code: "NE", languages: "French", flag: "flag-icon flag-icon-ne" },
                { name: "Nigeria", code: "NG", languages: "English", flag: "flag-icon flag-icon-ng" },
                { name: "Niue", code: "NU", languages: "Niuean, English", flag: "flag-icon flag-icon-nu" },
                { name: "Norfolk Island", code: "NF", languages: "English", flag: "flag-icon flag-icon-nf" },
                { name: "Northern Mariana Islands", code: "MP", languages: "English, Chamorro", flag: "flag-icon flag-icon-mp" },
                { name: "Norway", code: "NO", languages: "Norwegian", flag: "flag-icon flag-icon-no" },
                { name: "Oman", code: "OM", languages: "Arabic", flag: "flag-icon flag-icon-om" },
                { name: "Pakistan", code: "PK", languages: "Urdu, English", flag: "flag-icon flag-icon-pk" },
                { name: "Palau", code: "PW", languages: "English", flag: "flag-icon flag-icon-pw" },
                { name: "Palestine, State of", code: "PS", languages: "Arabic", flag: "flag-icon flag-icon-ps" },
                { name: "Panama", code: "PA", languages: "Spanish", flag: "flag-icon flag-icon-pa" },
                { name: "Papua New Guinea", code: "PG", languages: "English", flag: "flag-icon flag-icon-pg" },
                { name: "Paraguay", code: "PY", languages: "Spanish, Guaraní", flag: "flag-icon flag-icon-py" },
                { name: "Peru", code: "PE", languages: "Spanish", flag: "flag-icon flag-icon-pe" },
                { name: "Philippines", code: "PH", languages: "Filipino, English", flag: "flag-icon flag-icon-ph" },
                { name: "Pitcairn", code: "PN", languages: "English", flag: "flag-icon flag-icon-pn" },
                { name: "Poland", code: "PL", languages: "Polish", flag: "flag-icon flag-icon-pl" },
                { name: "Portugal", code: "PT", languages: "Portuguese", flag: "flag-icon flag-icon-pt" },
                { name: "Puerto Rico", code: "PR", languages: "Spanish, English", flag: "flag-icon flag-icon-pr" },
                { name: "Qatar", code: "QA", languages: "Arabic", flag: "flag-icon flag-icon-qa" },
                { name: "Réunion", code: "RE", languages: "French", flag: "flag-icon flag-icon-re" },
                { name: "Romania", code: "RO", languages: "Romanian", flag: "flag-icon flag-icon-ro" },
                { name: "Russian Federation", code: "RU", languages: "Russian", flag: "flag-icon flag-icon-ru" },
                { name: "Rwanda", code: "RW", languages: "Kinyarwanda, French, English", flag: "flag-icon flag-icon-rw" },
                { name: "Saint Barthélemy", code: "BL", languages: "French", flag: "flag-icon flag-icon-bl" },
                { name: "Saint Helena, Ascension and Tristan da Cunha", code: "SH", languages: "English", flag: "flag-icon flag-icon-sh" },
                { name: "Saint Kitts and Nevis", code: "KN", languages: "English", flag: "flag-icon flag-icon-kn" },
                { name: "Saint Lucia", code: "LC", languages: "English", flag: "flag-icon flag-icon-lc" },
                { name: "Saint Martin (French part)", code: "MF", languages: "French", flag: "flag-icon flag-icon-mf" },
                { name: "Saint Pierre and Miquelon", code: "PM", languages: "French", flag: "flag-icon flag-icon-pm" },
                { name: "Saint Vincent and the Grenadines", code: "VC", languages: "English", flag: "flag-icon flag-icon-vc" },
                { name: "Samoa", code: "WS", languages: "Samoan, English", flag: "flag-icon flag-icon-ws" },
                { name: "San Marino", code: "SM", languages: "Italian", flag: "flag-icon flag-icon-sm" },
                { name: "Sao Tome and Principe", code: "ST", languages: "Portuguese", flag: "flag-icon flag-icon-st" },
                { name: "Saudi Arabia", code: "SA", languages: "Arabic", flag: "flag-icon flag-icon-sa" },
                { name: "Senegal", code: "SN", languages: "French", flag: "flag-icon flag-icon-sn" },
                { name: "Serbia", code: "RS", languages: "Serbian", flag: "flag-icon flag-icon-rs" },
                { name: "Seychelles", code: "SC", languages: "English, French, Seychellois Creole", flag: "flag-icon flag-icon-sc" },
                { name: "Sierra Leone", code: "SL", languages: "English", flag: "flag-icon flag-icon-sl" },
                { name: "Singapore", code: "SG", languages: "English, Malay, Chinese, Tamil", flag: "flag-icon flag-icon-sg" },
                { name: "Sint Maarten (Dutch part)", code: "SX", languages: "Dutch, English", flag: "flag-icon flag-icon-sx" },
                { name: "Slovakia", code: "SK", languages: "Slovak", flag: "flag-icon flag-icon-sk" },
                { name: "Slovenia", code: "SI", languages: "Slovenian", flag: "flag-icon flag-icon-si" },
                { name: "Solomon Islands", code: "SB", languages: "English", flag: "flag-icon flag-icon-sb" },
                { name: "Somalia", code: "SO", languages: "Somali, Arabic", flag: "flag-icon flag-icon-so" },
                { name: "South Africa", code: "ZA", languages: "Zulu, Xhosa, Afrikaans, English", flag: "flag-icon flag-icon-za" },
                { name: "South Georgia and the South Sandwich Islands", code: "GS", languages: "English", flag: "flag-icon flag-icon-gs" },
                { name: "South Sudan", code: "SS", languages: "English", flag: "flag-icon flag-icon-ss" },
                { name: "Spain", code: "ES", languages: "Spanish", flag: "flag-icon flag-icon-es" },
                { name: "Sri Lanka", code: "LK", languages: "Sinhala, Tamil", flag: "flag-icon flag-icon-lk" },
                { name: "Sudan", code: "SD", languages: "Arabic, English", flag: "flag-icon flag-icon-sd" },
                { name: "Suriname", code: "SR", languages: "Dutch", flag: "flag-icon flag-icon-sr" },
                { name: "Svalbard and Jan Mayen", code: "SJ", languages: "Norwegian", flag: "flag-icon flag-icon-sj" },
                { name: "Swaziland", code: "SZ", languages: "English, Swazi", flag: "flag-icon flag-icon-sz" },
                { name: "Sweden", code: "SE", languages: "Swedish", flag: "flag-icon flag-icon-se" },
                { name: "Switzerland", code: "CH", languages: "German, French, Italian, Romansh", flag: "flag-icon flag-icon-ch" },
                { name: "Syrian Arab Republic", code: "SY", languages: "Arabic", flag: "flag-icon flag-icon-sy" },
                { name: "Taiwan, Province of China", code: "TW", languages: "Chinese", flag: "flag-icon flag-icon-tw" },
                { name: "Tajikistan", code: "TJ", languages: "Tajik, Russian", flag: "flag-icon flag-icon-tj" },
                { name: "Tanzania, United Republic of", code: "TZ", languages: "Swahili, English", flag: "flag-icon flag-icon-tz" },
                { name: "Thailand", code: "TH", languages: "Thai", flag: "flag-icon flag-icon-th" },
                { name: "Timor-Leste", code: "TL", languages: "Portuguese, Tetum", flag: "flag-icon flag-icon-tl" },
                { name: "Togo", code: "TG", languages: "French", flag: "flag-icon flag-icon-tg" },
                { name: "Tokelau", code: "TK", languages: "English, Tokelau", flag: "flag-icon flag-icon-tk" },
                { name: "Tonga", code: "TO", languages: "English, Tongan", flag: "flag-icon flag-icon-to" },
                { name: "Trinidad and Tobago", code: "TT", languages: "English", flag: "flag-icon flag-icon-tt" },
                { name: "Tunisia", code: "TN", languages: "Arabic", flag: "flag-icon flag-icon-tn" },
                { name: "Turkey", code: "TR", languages: "Turkish", flag: "flag-icon flag-icon-tr" },
                { name: "Turkmenistan", code: "TM", languages: "Turkmen, Russian", flag: "flag-icon flag-icon-tm" },
                { name: "Turks and Caicos Islands", code: "TC", languages: "English", flag: "flag-icon flag-icon-tc" },
                { name: "Tuvalu", code: "TV", languages: "English, Tuvalu", flag: "flag-icon flag-icon-tv" },
                { name: "Uganda", code: "UG", languages: "English, Swahili", flag: "flag-icon flag-icon-ug" },
                { name: "Ukraine", code: "UA", languages: "Ukrainian", flag: "flag-icon flag-icon-ua" },
                { name: "United Arab Emirates", code: "AE", languages: "Arabic", flag: "flag-icon flag-icon-ae" },
                { name: "United Kingdom", code: "GB", languages: "English", flag: "flag-icon flag-icon-gb" },
                { name: "United States", code: "US", languages: "English", flag: "flag-icon flag-icon-us" },
                { name: "United States Minor Outlying Islands", code: "UM", languages: "English", flag: "flag-icon flag-icon-um" },
                { name: "Uruguay", code: "UY", languages: "Spanish", flag: "flag-icon flag-icon-uy" },
                { name: "Uzbekistan", code: "UZ", languages: "Uzbek, Russian", flag: "flag-icon flag-icon-uz" },
                { name: "Vanuatu", code: "VU", languages: "Bislama, English, French", flag: "flag-icon flag-icon-vu" },
                { name: "Venezuela, Bolivarian Republic of", code: "VE", languages: "Spanish", flag: "flag-icon flag-icon-ve" },
                { name: "Viet Nam", code: "VN", languages: "Vietnamese", flag: "flag-icon flag-icon-vn" },
                { name: "Virgin Islands, British", code: "VG", languages: "English", flag: "flag-icon flag-icon-vg" },
                { name: "Virgin Islands, U.S.", code: "VI", languages: "English", flag: "flag-icon flag-icon-vi" },
                { name: "Wallis and Futuna", code: "WF", languages: "French", flag: "flag-icon flag-icon-wf" },
                { name: "Western Sahara", code: "EH", languages: "Arabic", flag: "flag-icon flag-icon-eh" },
                { name: "Yemen", code: "YE", languages: "Arabic", flag: "flag-icon flag-icon-ye" },
                { name: "Zambia", code: "ZM", languages: "English", flag: "flag-icon flag-icon-zm" },
                { name: "Zimbabwe", code: "ZW", languages: "English, Shona", flag: "flag-icon flag-icon-zw" },
            ],
            movies: [],
        }
    },

    methods: {
        // Declaring searchMovies method, inside which there's the API call
        searchMovies() {
            // Implemented API call to TMDB
            const options = {
                method: 'GET',
                headers: {
                    accept: 'application/json',
                    Authorization: 'Bearer eyJhbGciOiJIUzI1NiJ9.eyJhdWQiOiI4ZjYwMDQ3Y2RlYWZmNWM0NmYxZTc3MDdlMDc3YWY0MCIsInN1YiI6IjY0OTJjM2IxNjVlMGEyMDEyNWY5ZjgyZiIsInNjb3BlcyI6WyJhcGlfcmVhZCJdLCJ2ZXJzaW9uIjoxfQ.zuGfWxv_Hgil7FBEhmMq0e7sRe2NH5D0lXZnDpLTOV8'
                }
            };

            fetch(`https://api.themoviedb.org/3/search/movie?include_adult=false&language=en-US&page=1&query=${this.searchQuery}`, options)
                .then(response => response.json())
                .then(data => {
                    // We update the movie array with the results properties of the data object
                    this.movies = data.results;
                })
                .catch(err => console.error(err));
        },

        getFlagIcon(language) {
            return this.icons[language.toLowerCase()] || '';
        },

    }
}
</script>


<style lang="scss" scoped>
</style>    