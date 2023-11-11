<script setup>
import {FilterMatchMode, FilterService} from "primevue/api";
import moment from "moment-timezone";

const inputTime = ref(new Date());
const inputTimezone = ref({
  label: Intl.DateTimeFormat().resolvedOptions().timeZone,
  value: Intl.DateTimeFormat().resolvedOptions().timeZone,
});
const outputTimezone = ref(
    {
      label: Intl.DateTimeFormat().resolvedOptions().timeZone,
      value: Intl.DateTimeFormat().resolvedOptions().timeZone,
    }
);

const outputTime = computed(() => {
  if (outputTimezone.value?.value && inputTimezone.value?.value) {
    const inputTimezoneOffset = moment.tz(inputTime.value, inputTimezone.value.value).utcOffset();
    const outputTimezoneOffset = moment.tz(inputTime.value, outputTimezone.value.value).utcOffset();
    const diff = outputTimezoneOffset - inputTimezoneOffset;
    return moment(inputTime.value).add(diff, 'minutes').toDate();
  } else {
    return new Date();
  }
})

const timezones = [
  {
    "label": "Dateline Standard Time",
    "text": "(UTC-12:00) International Date Line West",
    "offset": -12,
    "abbr": "DST",
    "items": [
      {
        "label": "Etc/GMT+12",
        "value": "Etc/GMT+12"
      }
    ]
  },
  {
    "label": "UTC-11",
    "text": "(UTC-11:00) Coordinated Universal Time-11",
    "offset": -11,
    "abbr": "U",
    "items": [
      {
        "label": "Etc/GMT+11",
        "value": "Etc/GMT+11"
      },
      {
        "label": "Pacific/Midway",
        "value": "Pacific/Midway"
      },
      {
        "label": "Pacific/Niue",
        "value": "Pacific/Niue"
      },
      {
        "label": "Pacific/Pago_Pago",
        "value": "Pacific/Pago_Pago"
      }
    ]
  },
  {
    "label": "Hawaiian Standard Time",
    "text": "(UTC-10:00) Hawaii",
    "offset": -10,
    "abbr": "HST",
    "items": [
      {
        "label": "Etc/GMT+10",
        "value": "Etc/GMT+10"
      },
      {
        "label": "Pacific/Honolulu",
        "value": "Pacific/Honolulu"
      },
      {
        "label": "Pacific/Johnston",
        "value": "Pacific/Johnston"
      },
      {
        "label": "Pacific/Rarotonga",
        "value": "Pacific/Rarotonga"
      },
      {
        "label": "Pacific/Tahiti",
        "value": "Pacific/Tahiti"
      }
    ]
  },
  {
    "label": "Alaskan Standard Time",
    "text": "(UTC-09:00) Alaska",
    "offset": -8,
    "abbr": "AKDT",
    "items": [
      {
        "label": "America/Anchorage",
        "value": "America/Anchorage"
      },
      {
        "label": "America/Juneau",
        "value": "America/Juneau"
      },
      {
        "label": "America/Nome",
        "value": "America/Nome"
      },
      {
        "label": "America/Sitka",
        "value": "America/Sitka"
      },
      {
        "label": "America/Yakutat",
        "value": "America/Yakutat"
      }
    ]
  },
  {
    "label": "Pacific Standard Time (Mexico)",
    "text": "(UTC-08:00) Baja California",
    "offset": -7,
    "abbr": "PDT",
    "items": [
      {
        "label": "America/Santa_Isabel",
        "value": "America/Santa_Isabel"
      }
    ]
  },
  {
    "label": "Pacific Daylight Time",
    "text": "(UTC-07:00) Pacific Daylight Time (US & Canada)",
    "offset": -7,
    "abbr": "PDT",
    "items": [
      {
        "label": "America/Los_Angeles",
        "value": "America/Los_Angeles"
      },
      {
        "label": "America/Tijuana",
        "value": "America/Tijuana"
      },
      {
        "label": "America/Vancouver",
        "value": "America/Vancouver"
      }
    ]
  },
  {
    "label": "Pacific Standard Time",
    "text": "(UTC-08:00) Pacific Standard Time (US & Canada)",
    "offset": -8,
    "abbr": "PST",
    "items": [
      {
        "label": "America/Los_Angeles",
        "value": "America/Los_Angeles"
      },
      {
        "label": "America/Tijuana",
        "value": "America/Tijuana"
      },
      {
        "label": "America/Vancouver",
        "value": "America/Vancouver"
      },
      {
        "label": "PST8PDT",
        "value": "PST8PDT"
      }
    ]
  },
  {
    "label": "US Mountain Standard Time",
    "text": "(UTC-07:00) Arizona",
    "offset": -7,
    "abbr": "UMST",
    "items": [
      {
        "label": "America/Creston",
        "value": "America/Creston"
      },
      {
        "label": "America/Dawson",
        "value": "America/Dawson"
      },
      {
        "label": "America/Dawson_Creek",
        "value": "America/Dawson_Creek"
      },
      {
        "label": "America/Hermosillo",
        "value": "America/Hermosillo"
      },
      {
        "label": "America/Phoenix",
        "value": "America/Phoenix"
      },
      {
        "label": "America/Whitehorse",
        "value": "America/Whitehorse"
      },
      {
        "label": "Etc/GMT+7",
        "value": "Etc/GMT+7"
      }
    ]
  },
  {
    "label": "Mountain Standard Time (Mexico)",
    "text": "(UTC-07:00) Chihuahua, La Paz, Mazatlan",
    "offset": -6,
    "abbr": "MDT",
    "items": [
      {
        "label": "America/Chihuahua",
        "value": "America/Chihuahua"
      },
      {
        "label": "America/Mazatlan",
        "value": "America/Mazatlan"
      }
    ]
  },
  {
    "label": "Mountain Standard Time",
    "text": "(UTC-07:00) Mountain Time (US & Canada)",
    "offset": -6,
    "abbr": "MDT",
    "items": [
      {
        "label": "America/Boise",
        "value": "America/Boise"
      },
      {
        "label": "America/Cambridge_Bay",
        "value": "America/Cambridge_Bay"
      },
      {
        "label": "America/Denver",
        "value": "America/Denver"
      },
      {
        "label": "America/Edmonton",
        "value": "America/Edmonton"
      },
      {
        "label": "America/Inuvik",
        "value": "America/Inuvik"
      },
      {
        "label": "America/Ojinaga",
        "value": "America/Ojinaga"
      },
      {
        "label": "America/Yellowknife",
        "value": "America/Yellowknife"
      },
      {
        "label": "MST7MDT",
        "value": "MST7MDT"
      }
    ]
  },
  {
    "label": "Central America Standard Time",
    "text": "(UTC-06:00) Central America",
    "offset": -6,
    "abbr": "CAST",
    "items": [
      {
        "label": "America/Belize",
        "value": "America/Belize"
      },
      {
        "label": "America/Costa_Rica",
        "value": "America/Costa_Rica"
      },
      {
        "label": "America/El_Salvador",
        "value": "America/El_Salvador"
      },
      {
        "label": "America/Guatemala",
        "value": "America/Guatemala"
      },
      {
        "label": "America/Managua",
        "value": "America/Managua"
      },
      {
        "label": "America/Tegucigalpa",
        "value": "America/Tegucigalpa"
      },
      {
        "label": "Etc/GMT+6",
        "value": "Etc/GMT+6"
      },
      {
        "label": "Pacific/Galapagos",
        "value": "Pacific/Galapagos"
      }
    ]
  },
  {
    "label": "Central Standard Time",
    "text": "(UTC-06:00) Central Time (US & Canada)",
    "offset": -5,
    "abbr": "CDT",
    "items": [
      {
        "label": "America/Chicago",
        "value": "America/Chicago"
      },
      {
        "label": "America/Indiana/Knox",
        "value": "America/Indiana/Knox"
      },
      {
        "label": "America/Indiana/Tell_City",
        "value": "America/Indiana/Tell_City"
      },
      {
        "label": "America/Matamoros",
        "value": "America/Matamoros"
      },
      {
        "label": "America/Menominee",
        "value": "America/Menominee"
      },
      {
        "label": "America/North_Dakota/Beulah",
        "value": "America/North_Dakota/Beulah"
      },
      {
        "label": "America/North_Dakota/Center",
        "value": "America/North_Dakota/Center"
      },
      {
        "label": "America/North_Dakota/New_Salem",
        "value": "America/North_Dakota/New_Salem"
      },
      {
        "label": "America/Rainy_River",
        "value": "America/Rainy_River"
      },
      {
        "label": "America/Rankin_Inlet",
        "value": "America/Rankin_Inlet"
      },
      {
        "label": "America/Resolute",
        "value": "America/Resolute"
      },
      {
        "label": "America/Winnipeg",
        "value": "America/Winnipeg"
      },
      {
        "label": "CST6CDT",
        "value": "CST6CDT"
      }
    ]
  },
  {
    "label": "Central Standard Time (Mexico)",
    "text": "(UTC-06:00) Guadalajara, Mexico City, Monterrey",
    "offset": -5,
    "abbr": "CDT",
    "items": [
      {
        "label": "America/Bahia_Banderas",
        "value": "America/Bahia_Banderas"
      },
      {
        "label": "America/Cancun",
        "value": "America/Cancun"
      },
      {
        "label": "America/Merida",
        "value": "America/Merida"
      },
      {
        "label": "America/Mexico_City",
        "value": "America/Mexico_City"
      },
      {
        "label": "America/Monterrey",
        "value": "America/Monterrey"
      }
    ]
  },
  {
    "label": "Canada Central Standard Time",
    "text": "(UTC-06:00) Saskatchewan",
    "offset": -6,
    "abbr": "CCST",
    "items": [
      {
        "label": "America/Regina",
        "value": "America/Regina"
      },
      {
        "label": "America/Swift_Current",
        "value": "America/Swift_Current"
      }
    ]
  },
  {
    "label": "SA Pacific Standard Time",
    "text": "(UTC-05:00) Bogota, Lima, Quito",
    "offset": -5,
    "abbr": "SPST",
    "items": [
      {
        "label": "America/Bogota",
        "value": "America/Bogota"
      },
      {
        "label": "America/Cayman",
        "value": "America/Cayman"
      },
      {
        "label": "America/Coral_Harbour",
        "value": "America/Coral_Harbour"
      },
      {
        "label": "America/Eirunepe",
        "value": "America/Eirunepe"
      },
      {
        "label": "America/Guayaquil",
        "value": "America/Guayaquil"
      },
      {
        "label": "America/Jamaica",
        "value": "America/Jamaica"
      },
      {
        "label": "America/Lima",
        "value": "America/Lima"
      },
      {
        "label": "America/Panama",
        "value": "America/Panama"
      },
      {
        "label": "America/Rio_Branco",
        "value": "America/Rio_Branco"
      },
      {
        "label": "Etc/GMT+5",
        "value": "Etc/GMT+5"
      }
    ]
  },
  {
    "label": "Eastern Standard Time",
    "text": "(UTC-05:00) Eastern Time (US & Canada)",
    "offset": -5,
    "abbr": "EST",
    "items": [
      {
        "label": "America/Detroit",
        "value": "America/Detroit"
      },
      {
        "label": "America/Havana",
        "value": "America/Havana"
      },
      {
        "label": "America/Indiana/Petersburg",
        "value": "America/Indiana/Petersburg"
      },
      {
        "label": "America/Indiana/Vincennes",
        "value": "America/Indiana/Vincennes"
      },
      {
        "label": "America/Indiana/Winamac",
        "value": "America/Indiana/Winamac"
      },
      {
        "label": "America/Iqaluit",
        "value": "America/Iqaluit"
      },
      {
        "label": "America/Kentucky/Monticello",
        "value": "America/Kentucky/Monticello"
      },
      {
        "label": "America/Louisville",
        "value": "America/Louisville"
      },
      {
        "label": "America/Montreal",
        "value": "America/Montreal"
      },
      {
        "label": "America/Nassau",
        "value": "America/Nassau"
      },
      {
        "label": "America/New_York",
        "value": "America/New_York"
      },
      {
        "label": "America/Nipigon",
        "value": "America/Nipigon"
      },
      {
        "label": "America/Pangnirtung",
        "value": "America/Pangnirtung"
      },
      {
        "label": "America/Port-au-Prince",
        "value": "America/Port-au-Prince"
      },
      {
        "label": "America/Thunder_Bay",
        "value": "America/Thunder_Bay"
      },
      {
        "label": "America/Toronto",
        "value": "America/Toronto"
      }
    ]
  },
  {
    "label": "Eastern Daylight Time",
    "text": "(UTC-04:00) Eastern Daylight Time (US & Canada)",
    "offset": -4,
    "abbr": "EDT",
    "items": [
      {
        "label": "America/Detroit",
        "value": "America/Detroit"
      },
      {
        "label": "America/Havana",
        "value": "America/Havana"
      },
      {
        "label": "America/Indiana/Petersburg",
        "value": "America/Indiana/Petersburg"
      },
      {
        "label": "America/Indiana/Vincennes",
        "value": "America/Indiana/Vincennes"
      },
      {
        "label": "America/Indiana/Winamac",
        "value": "America/Indiana/Winamac"
      },
      {
        "label": "America/Iqaluit",
        "value": "America/Iqaluit"
      },
      {
        "label": "America/Kentucky/Monticello",
        "value": "America/Kentucky/Monticello"
      },
      {
        "label": "America/Louisville",
        "value": "America/Louisville"
      },
      {
        "label": "America/Montreal",
        "value": "America/Montreal"
      },
      {
        "label": "America/Nassau",
        "value": "America/Nassau"
      },
      {
        "label": "America/New_York",
        "value": "America/New_York"
      },
      {
        "label": "America/Nipigon",
        "value": "America/Nipigon"
      },
      {
        "label": "America/Pangnirtung",
        "value": "America/Pangnirtung"
      },
      {
        "label": "America/Port-au-Prince",
        "value": "America/Port-au-Prince"
      },
      {
        "label": "America/Thunder_Bay",
        "value": "America/Thunder_Bay"
      },
      {
        "label": "America/Toronto",
        "value": "America/Toronto"
      }
    ]
  },
  {
    "label": "US Eastern Standard Time",
    "text": "(UTC-05:00) Indiana (East)",
    "offset": -5,
    "abbr": "UEDT",
    "items": [
      {
        "label": "America/Indiana/Marengo",
        "value": "America/Indiana/Marengo"
      },
      {
        "label": "America/Indiana/Vevay",
        "value": "America/Indiana/Vevay"
      },
      {
        "label": "America/Indianapolis",
        "value": "America/Indianapolis"
      }
    ]
  },
  {
    "label": "Venezuela Standard Time",
    "text": "(UTC-04:30) Caracas",
    "offset": -4.5,
    "abbr": "VST",
    "items": [
      {
        "label": "America/Caracas",
        "value": "America/Caracas"
      }
    ]
  },
  {
    "label": "Paraguay Standard Time",
    "text": "(UTC-04:00) Asuncion",
    "offset": -4,
    "abbr": "PYT",
    "items": [
      {
        "label": "America/Asuncion",
        "value": "America/Asuncion"
      }
    ]
  },
  {
    "label": "Atlantic Standard Time",
    "text": "(UTC-04:00) Atlantic Time (Canada)",
    "offset": -3,
    "abbr": "ADT",
    "items": [
      {
        "label": "America/Glace_Bay",
        "value": "America/Glace_Bay"
      },
      {
        "label": "America/Goose_Bay",
        "value": "America/Goose_Bay"
      },
      {
        "label": "America/Halifax",
        "value": "America/Halifax"
      },
      {
        "label": "America/Moncton",
        "value": "America/Moncton"
      },
      {
        "label": "America/Thule",
        "value": "America/Thule"
      },
      {
        "label": "Atlantic/Bermuda",
        "value": "Atlantic/Bermuda"
      }
    ]
  },
  {
    "label": "Central Brazilian Standard Time",
    "text": "(UTC-04:00) Cuiaba",
    "offset": -4,
    "abbr": "CBST",
    "items": [
      {
        "label": "America/Campo_Grande",
        "value": "America/Campo_Grande"
      },
      {
        "label": "America/Cuiaba",
        "value": "America/Cuiaba"
      }
    ]
  },
  {
    "label": "SA Western Standard Time",
    "text": "(UTC-04:00) Georgetown, La Paz, Manaus, San Juan",
    "offset": -4,
    "abbr": "SWST",
    "items": [
      {
        "label": "America/Anguilla",
        "value": "America/Anguilla"
      },
      {
        "label": "America/Antigua",
        "value": "America/Antigua"
      },
      {
        "label": "America/Aruba",
        "value": "America/Aruba"
      },
      {
        "label": "America/Barbados",
        "value": "America/Barbados"
      },
      {
        "label": "America/Blanc-Sablon",
        "value": "America/Blanc-Sablon"
      },
      {
        "label": "America/Boa_Vista",
        "value": "America/Boa_Vista"
      },
      {
        "label": "America/Curacao",
        "value": "America/Curacao"
      },
      {
        "label": "America/Dominica",
        "value": "America/Dominica"
      },
      {
        "label": "America/Grand_Turk",
        "value": "America/Grand_Turk"
      },
      {
        "label": "America/Grenada",
        "value": "America/Grenada"
      },
      {
        "label": "America/Guadeloupe",
        "value": "America/Guadeloupe"
      },
      {
        "label": "America/Guyana",
        "value": "America/Guyana"
      },
      {
        "label": "America/Kralendijk",
        "value": "America/Kralendijk"
      },
      {
        "label": "America/La_Paz",
        "value": "America/La_Paz"
      },
      {
        "label": "America/Lower_Princes",
        "value": "America/Lower_Princes"
      },
      {
        "label": "America/Manaus",
        "value": "America/Manaus"
      },
      {
        "label": "America/Marigot",
        "value": "America/Marigot"
      },
      {
        "label": "America/Martinique",
        "value": "America/Martinique"
      },
      {
        "label": "America/Montserrat",
        "value": "America/Montserrat"
      },
      {
        "label": "America/Port_of_Spain",
        "value": "America/Port_of_Spain"
      },
      {
        "label": "America/Porto_Velho",
        "value": "America/Porto_Velho"
      },
      {
        "label": "America/Puerto_Rico",
        "value": "America/Puerto_Rico"
      },
      {
        "label": "America/Santo_Domingo",
        "value": "America/Santo_Domingo"
      },
      {
        "label": "America/St_Barthelemy",
        "value": "America/St_Barthelemy"
      },
      {
        "label": "America/St_Kitts",
        "value": "America/St_Kitts"
      },
      {
        "label": "America/St_Lucia",
        "value": "America/St_Lucia"
      },
      {
        "label": "America/St_Thomas",
        "value": "America/St_Thomas"
      },
      {
        "label": "America/St_Vincent",
        "value": "America/St_Vincent"
      },
      {
        "label": "America/Tortola",
        "value": "America/Tortola"
      },
      {
        "label": "Etc/GMT+4",
        "value": "Etc/GMT+4"
      }
    ]
  },
  {
    "label": "Pacific SA Standard Time",
    "text": "(UTC-04:00) Santiago",
    "offset": -4,
    "abbr": "PSST",
    "items": [
      {
        "label": "America/Santiago",
        "value": "America/Santiago"
      },
      {
        "label": "Antarctica/Palmer",
        "value": "Antarctica/Palmer"
      }
    ]
  },
  {
    "label": "Newfoundland Standard Time",
    "text": "(UTC-03:30) Newfoundland",
    "offset": -2.5,
    "abbr": "NDT",
    "items": [
      {
        "label": "America/St_Johns",
        "value": "America/St_Johns"
      }
    ]
  },
  {
    "label": "E. South America Standard Time",
    "text": "(UTC-03:00) Brasilia",
    "offset": -3,
    "abbr": "ESAST",
    "items": [
      {
        "label": "America/Sao_Paulo",
        "value": "America/Sao_Paulo"
      }
    ]
  },
  {
    "label": "Argentina Standard Time",
    "text": "(UTC-03:00) Buenos Aires",
    "offset": -3,
    "abbr": "AST",
    "items": [
      {
        "label": "America/Argentina/Buenos_Aires",
        "value": "America/Argentina/Buenos_Aires"
      },
      {
        "label": "America/Argentina/Catamarca",
        "value": "America/Argentina/Catamarca"
      },
      {
        "label": "America/Argentina/Cordoba",
        "value": "America/Argentina/Cordoba"
      },
      {
        "label": "America/Argentina/Jujuy",
        "value": "America/Argentina/Jujuy"
      },
      {
        "label": "America/Argentina/La_Rioja",
        "value": "America/Argentina/La_Rioja"
      },
      {
        "label": "America/Argentina/Mendoza",
        "value": "America/Argentina/Mendoza"
      },
      {
        "label": "America/Argentina/Rio_Gallegos",
        "value": "America/Argentina/Rio_Gallegos"
      },
      {
        "label": "America/Argentina/Salta",
        "value": "America/Argentina/Salta"
      },
      {
        "label": "America/Argentina/San_Juan",
        "value": "America/Argentina/San_Juan"
      },
      {
        "label": "America/Argentina/San_Luis",
        "value": "America/Argentina/San_Luis"
      },
      {
        "label": "America/Argentina/Tucuman",
        "value": "America/Argentina/Tucuman"
      },
      {
        "label": "America/Argentina/Ushuaia",
        "value": "America/Argentina/Ushuaia"
      },
      {
        "label": "America/Buenos_Aires",
        "value": "America/Buenos_Aires"
      },
      {
        "label": "America/Catamarca",
        "value": "America/Catamarca"
      },
      {
        "label": "America/Cordoba",
        "value": "America/Cordoba"
      },
      {
        "label": "America/Jujuy",
        "value": "America/Jujuy"
      },
      {
        "label": "America/Mendoza",
        "value": "America/Mendoza"
      }
    ]
  },
  {
    "label": "SA Eastern Standard Time",
    "text": "(UTC-03:00) Cayenne, Fortaleza",
    "offset": -3,
    "abbr": "SEST",
    "items": [
      {
        "label": "America/Araguaina",
        "value": "America/Araguaina"
      },
      {
        "label": "America/Belem",
        "value": "America/Belem"
      },
      {
        "label": "America/Cayenne",
        "value": "America/Cayenne"
      },
      {
        "label": "America/Fortaleza",
        "value": "America/Fortaleza"
      },
      {
        "label": "America/Maceio",
        "value": "America/Maceio"
      },
      {
        "label": "America/Paramaribo",
        "value": "America/Paramaribo"
      },
      {
        "label": "America/Recife",
        "value": "America/Recife"
      },
      {
        "label": "America/Santarem",
        "value": "America/Santarem"
      },
      {
        "label": "Antarctica/Rothera",
        "value": "Antarctica/Rothera"
      },
      {
        "label": "Atlantic/Stanley",
        "value": "Atlantic/Stanley"
      },
      {
        "label": "Etc/GMT+3",
        "value": "Etc/GMT+3"
      }
    ]
  },
  {
    "label": "Greenland Standard Time",
    "text": "(UTC-03:00) Greenland",
    "offset": -3,
    "abbr": "GDT",
    "items": [
      {
        "label": "America/Godthab",
        "value": "America/Godthab"
      }
    ]
  },
  {
    "label": "Montevideo Standard Time",
    "text": "(UTC-03:00) Montevideo",
    "offset": -3,
    "abbr": "MST",
    "items": [
      {
        "label": "America/Montevideo",
        "value": "America/Montevideo"
      }
    ]
  },
  {
    "label": "Bahia Standard Time",
    "text": "(UTC-03:00) Salvador",
    "offset": -3,
    "abbr": "BST",
    "items": [
      {
        "label": "America/Bahia",
        "value": "America/Bahia"
      }
    ]
  },
  {
    "label": "UTC-02",
    "text": "(UTC-02:00) Coordinated Universal Time-02",
    "offset": -2,
    "abbr": "U",
    "items": [
      {
        "label": "America/Noronha",
        "value": "America/Noronha"
      },
      {
        "label": "Atlantic/South_Georgia",
        "value": "Atlantic/South_Georgia"
      },
      {
        "label": "Etc/GMT+2",
        "value": "Etc/GMT+2"
      }
    ]
  },
  {
    "label": "Mid-Atlantic Standard Time",
    "text": "(UTC-02:00) Mid-Atlantic - Old",
    "offset": -1,
    "abbr": "MDT",
    "items": []
  },
  {
    "label": "Azores Standard Time",
    "text": "(UTC-01:00) Azores",
    "offset": 0,
    "abbr": "ADT",
    "items": [
      {
        "label": "America/Scoresbysund",
        "value": "America/Scoresbysund"
      },
      {
        "label": "Atlantic/Azores",
        "value": "Atlantic/Azores"
      }
    ]
  },
  {
    "label": "Cape Verde Standard Time",
    "text": "(UTC-01:00) Cape Verde Is.",
    "offset": -1,
    "abbr": "CVST",
    "items": [
      {
        "label": "Atlantic/Cape_Verde",
        "value": "Atlantic/Cape_Verde"
      },
      {
        "label": "Etc/GMT+1",
        "value": "Etc/GMT+1"
      }
    ]
  },
  {
    "label": "Morocco Standard Time",
    "text": "(UTC) Casablanca",
    "offset": 1,
    "abbr": "MDT",
    "items": [
      {
        "label": "Africa/Casablanca",
        "value": "Africa/Casablanca"
      },
      {
        "label": "Africa/El_Aaiun",
        "value": "Africa/El_Aaiun"
      }
    ]
  },
  {
    "label": "UTC",
    "text": "(UTC) Coordinated Universal Time",
    "offset": 0,
    "abbr": "UTC",
    "items": [
      {
        "label": "America/Danmarkshavn",
        "value": "America/Danmarkshavn"
      },
      {
        "label": "Etc/GMT",
        "value": "Etc/GMT"
      }
    ]
  },
  {
    "label": "GMT Standard Time",
    "text": "(UTC) Edinburgh, London",
    "offset": 0,
    "abbr": "GMT",
    "items": [
      {
        "label": "Europe/Isle_of_Man",
        "value": "Europe/Isle_of_Man"
      },
      {
        "label": "Europe/Guernsey",
        "value": "Europe/Guernsey"
      },
      {
        "label": "Europe/Jersey",
        "value": "Europe/Jersey"
      },
      {
        "label": "Europe/London",
        "value": "Europe/London"
      }
    ]
  },
  {
    "label": "British Summer Time",
    "text": "(UTC+01:00) Edinburgh, London",
    "offset": 1,
    "abbr": "BST",
    "items": [
      {
        "label": "Europe/Isle_of_Man",
        "value": "Europe/Isle_of_Man"
      },
      {
        "label": "Europe/Guernsey",
        "value": "Europe/Guernsey"
      },
      {
        "label": "Europe/Jersey",
        "value": "Europe/Jersey"
      },
      {
        "label": "Europe/London",
        "value": "Europe/London"
      }
    ]
  },
  {
    "label": "GMT Standard Time",
    "text": "(UTC) Dublin, Lisbon",
    "offset": 1,
    "abbr": "GDT",
    "items": [
      {
        "label": "Atlantic/Canary",
        "value": "Atlantic/Canary"
      },
      {
        "label": "Atlantic/Faeroe",
        "value": "Atlantic/Faeroe"
      },
      {
        "label": "Atlantic/Madeira",
        "value": "Atlantic/Madeira"
      },
      {
        "label": "Europe/Dublin",
        "value": "Europe/Dublin"
      },
      {
        "label": "Europe/Lisbon",
        "value": "Europe/Lisbon"
      }
    ]
  },
  {
    "label": "Greenwich Standard Time",
    "text": "(UTC) Monrovia, Reykjavik",
    "offset": 0,
    "abbr": "GST",
    "items": [
      {
        "label": "Africa/Abidjan",
        "value": "Africa/Abidjan"
      },
      {
        "label": "Africa/Accra",
        "value": "Africa/Accra"
      },
      {
        "label": "Africa/Bamako",
        "value": "Africa/Bamako"
      },
      {
        "label": "Africa/Banjul",
        "value": "Africa/Banjul"
      },
      {
        "label": "Africa/Bissau",
        "value": "Africa/Bissau"
      },
      {
        "label": "Africa/Conakry",
        "value": "Africa/Conakry"
      },
      {
        "label": "Africa/Dakar",
        "value": "Africa/Dakar"
      },
      {
        "label": "Africa/Freetown",
        "value": "Africa/Freetown"
      },
      {
        "label": "Africa/Lome",
        "value": "Africa/Lome"
      },
      {
        "label": "Africa/Monrovia",
        "value": "Africa/Monrovia"
      },
      {
        "label": "Africa/Nouakchott",
        "value": "Africa/Nouakchott"
      },
      {
        "label": "Africa/Ouagadougou",
        "value": "Africa/Ouagadougou"
      },
      {
        "label": "Africa/Sao_Tome",
        "value": "Africa/Sao_Tome"
      },
      {
        "label": "Atlantic/Reykjavik",
        "value": "Atlantic/Reykjavik"
      },
      {
        "label": "Atlantic/St_Helena",
        "value": "Atlantic/St_Helena"
      }
    ]
  },
  {
    "label": "W. Europe Standard Time",
    "text": "(UTC+01:00) Amsterdam, Berlin, Bern, Rome, Stockholm, Vienna",
    "offset": 2,
    "abbr": "WEDT",
    "items": [
      {
        "label": "Arctic/Longyearbyen",
        "value": "Arctic/Longyearbyen"
      },
      {
        "label": "Europe/Amsterdam",
        "value": "Europe/Amsterdam"
      },
      {
        "label": "Europe/Andorra",
        "value": "Europe/Andorra"
      },
      {
        "label": "Europe/Berlin",
        "value": "Europe/Berlin"
      },
      {
        "label": "Europe/Busingen",
        "value": "Europe/Busingen"
      },
      {
        "label": "Europe/Gibraltar",
        "value": "Europe/Gibraltar"
      },
      {
        "label": "Europe/Luxembourg",
        "value": "Europe/Luxembourg"
      },
      {
        "label": "Europe/Malta",
        "value": "Europe/Malta"
      },
      {
        "label": "Europe/Monaco",
        "value": "Europe/Monaco"
      },
      {
        "label": "Europe/Oslo",
        "value": "Europe/Oslo"
      },
      {
        "label": "Europe/Rome",
        "value": "Europe/Rome"
      },
      {
        "label": "Europe/San_Marino",
        "value": "Europe/San_Marino"
      },
      {
        "label": "Europe/Stockholm",
        "value": "Europe/Stockholm"
      },
      {
        "label": "Europe/Vaduz",
        "value": "Europe/Vaduz"
      },
      {
        "label": "Europe/Vatican",
        "value": "Europe/Vatican"
      },
      {
        "label": "Europe/Vienna",
        "value": "Europe/Vienna"
      },
      {
        "label": "Europe/Zurich",
        "value": "Europe/Zurich"
      }
    ]
  },
  {
    "label": "Central Europe Standard Time",
    "text": "(UTC+01:00) Belgrade, Bratislava, Budapest, Ljubljana, Prague",
    "offset": 2,
    "abbr": "CEDT",
    "items": [
      {
        "label": "Europe/Belgrade",
        "value": "Europe/Belgrade"
      },
      {
        "label": "Europe/Bratislava",
        "value": "Europe/Bratislava"
      },
      {
        "label": "Europe/Budapest",
        "value": "Europe/Budapest"
      },
      {
        "label": "Europe/Ljubljana",
        "value": "Europe/Ljubljana"
      },
      {
        "label": "Europe/Podgorica",
        "value": "Europe/Podgorica"
      },
      {
        "label": "Europe/Prague",
        "value": "Europe/Prague"
      },
      {
        "label": "Europe/Tirane",
        "value": "Europe/Tirane"
      }
    ]
  },
  {
    "label": "Romance Standard Time",
    "text": "(UTC+01:00) Brussels, Copenhagen, Madrid, Paris",
    "offset": 2,
    "abbr": "RDT",
    "items": [
      {
        "label": "Africa/Ceuta",
        "value": "Africa/Ceuta"
      },
      {
        "label": "Europe/Brussels",
        "value": "Europe/Brussels"
      },
      {
        "label": "Europe/Copenhagen",
        "value": "Europe/Copenhagen"
      },
      {
        "label": "Europe/Madrid",
        "value": "Europe/Madrid"
      },
      {
        "label": "Europe/Paris",
        "value": "Europe/Paris"
      }
    ]
  },
  {
    "label": "Central European Standard Time",
    "text": "(UTC+01:00) Sarajevo, Skopje, Warsaw, Zagreb",
    "offset": 2,
    "abbr": "CEDT",
    "items": [
      {
        "label": "Europe/Sarajevo",
        "value": "Europe/Sarajevo"
      },
      {
        "label": "Europe/Skopje",
        "value": "Europe/Skopje"
      },
      {
        "label": "Europe/Warsaw",
        "value": "Europe/Warsaw"
      },
      {
        "label": "Europe/Zagreb",
        "value": "Europe/Zagreb"
      }
    ]
  },
  {
    "label": "W. Central Africa Standard Time",
    "text": "(UTC+01:00) West Central Africa",
    "offset": 1,
    "abbr": "WCAST",
    "items": [
      {
        "label": "Africa/Algiers",
        "value": "Africa/Algiers"
      },
      {
        "label": "Africa/Bangui",
        "value": "Africa/Bangui"
      },
      {
        "label": "Africa/Brazzaville",
        "value": "Africa/Brazzaville"
      },
      {
        "label": "Africa/Douala",
        "value": "Africa/Douala"
      },
      {
        "label": "Africa/Kinshasa",
        "value": "Africa/Kinshasa"
      },
      {
        "label": "Africa/Lagos",
        "value": "Africa/Lagos"
      },
      {
        "label": "Africa/Libreville",
        "value": "Africa/Libreville"
      },
      {
        "label": "Africa/Luanda",
        "value": "Africa/Luanda"
      },
      {
        "label": "Africa/Malabo",
        "value": "Africa/Malabo"
      },
      {
        "label": "Africa/Ndjamena",
        "value": "Africa/Ndjamena"
      },
      {
        "label": "Africa/Niamey",
        "value": "Africa/Niamey"
      },
      {
        "label": "Africa/Porto-Novo",
        "value": "Africa/Porto-Novo"
      },
      {
        "label": "Africa/Tunis",
        "value": "Africa/Tunis"
      },
      {
        "label": "Etc/GMT-1",
        "value": "Etc/GMT-1"
      }
    ]
  },
  {
    "label": "Namibia Standard Time",
    "text": "(UTC+01:00) Windhoek",
    "offset": 1,
    "abbr": "NST",
    "items": [
      {
        "label": "Africa/Windhoek",
        "value": "Africa/Windhoek"
      }
    ]
  },
  {
    "label": "GTB Standard Time",
    "text": "(UTC+02:00) Athens, Bucharest",
    "offset": 3,
    "abbr": "GDT",
    "items": [
      {
        "label": "Asia/Nicosia",
        "value": "Asia/Nicosia"
      },
      {
        "label": "Europe/Athens",
        "value": "Europe/Athens"
      },
      {
        "label": "Europe/Bucharest",
        "value": "Europe/Bucharest"
      },
      {
        "label": "Europe/Chisinau",
        "value": "Europe/Chisinau"
      }
    ]
  },
  {
    "label": "Middle East Standard Time",
    "text": "(UTC+02:00) Beirut",
    "offset": 3,
    "abbr": "MEDT",
    "items": [
      {
        "label": "Asia/Beirut",
        "value": "Asia/Beirut"
      }
    ]
  },
  {
    "label": "Egypt Standard Time",
    "text": "(UTC+02:00) Cairo",
    "offset": 2,
    "abbr": "EST",
    "items": [
      {
        "label": "Africa/Cairo",
        "value": "Africa/Cairo"
      }
    ]
  },
  {
    "label": "Syria Standard Time",
    "text": "(UTC+02:00) Damascus",
    "offset": 3,
    "abbr": "SDT",
    "items": [
      {
        "label": "Asia/Damascus",
        "value": "Asia/Damascus"
      }
    ]
  },
  {
    "label": "E. Europe Standard Time",
    "text": "(UTC+02:00) E. Europe",
    "offset": 3,
    "abbr": "EEDT",
    "items": [
      {
        "label": "Asia/Nicosia",
        "value": "Asia/Nicosia"
      },
      {
        "label": "Europe/Athens",
        "value": "Europe/Athens"
      },
      {
        "label": "Europe/Bucharest",
        "value": "Europe/Bucharest"
      },
      {
        "label": "Europe/Chisinau",
        "value": "Europe/Chisinau"
      },
      {
        "label": "Europe/Helsinki",
        "value": "Europe/Helsinki"
      },
      {
        "label": "Europe/Kyiv",
        "value": "Europe/Kyiv"
      },
      {
        "label": "Europe/Mariehamn",
        "value": "Europe/Mariehamn"
      },
      {
        "label": "Europe/Nicosia",
        "value": "Europe/Nicosia"
      },
      {
        "label": "Europe/Riga",
        "value": "Europe/Riga"
      },
      {
        "label": "Europe/Sofia",
        "value": "Europe/Sofia"
      },
      {
        "label": "Europe/Tallinn",
        "value": "Europe/Tallinn"
      },
      {
        "label": "Europe/Uzhgorod",
        "value": "Europe/Uzhgorod"
      },
      {
        "label": "Europe/Vilnius",
        "value": "Europe/Vilnius"
      },
      {
        "label": "Europe/Zaporozhye",
        "value": "Europe/Zaporozhye"
      }
    ]
  },
  {
    "label": "South Africa Standard Time",
    "text": "(UTC+02:00) Harare, Pretoria",
    "offset": 2,
    "abbr": "SAST",
    "items": [
      {
        "label": "Africa/Blantyre",
        "value": "Africa/Blantyre"
      },
      {
        "label": "Africa/Bujumbura",
        "value": "Africa/Bujumbura"
      },
      {
        "label": "Africa/Gaborone",
        "value": "Africa/Gaborone"
      },
      {
        "label": "Africa/Harare",
        "value": "Africa/Harare"
      },
      {
        "label": "Africa/Johannesburg",
        "value": "Africa/Johannesburg"
      },
      {
        "label": "Africa/Kigali",
        "value": "Africa/Kigali"
      },
      {
        "label": "Africa/Lubumbashi",
        "value": "Africa/Lubumbashi"
      },
      {
        "label": "Africa/Lusaka",
        "value": "Africa/Lusaka"
      },
      {
        "label": "Africa/Maputo",
        "value": "Africa/Maputo"
      },
      {
        "label": "Africa/Maseru",
        "value": "Africa/Maseru"
      },
      {
        "label": "Africa/Mbabane",
        "value": "Africa/Mbabane"
      },
      {
        "label": "Etc/GMT-2",
        "value": "Etc/GMT-2"
      }
    ]
  },
  {
    "label": "FLE Standard Time",
    "text": "(UTC+02:00) Helsinki, Kyiv, Riga, Sofia, Tallinn, Vilnius",
    "offset": 3,
    "abbr": "FDT",
    "items": [
      {
        "label": "Europe/Helsinki",
        "value": "Europe/Helsinki"
      },
      {
        "label": "Europe/Kyiv",
        "value": "Europe/Kyiv"
      },
      {
        "label": "Europe/Mariehamn",
        "value": "Europe/Mariehamn"
      },
      {
        "label": "Europe/Riga",
        "value": "Europe/Riga"
      },
      {
        "label": "Europe/Sofia",
        "value": "Europe/Sofia"
      },
      {
        "label": "Europe/Tallinn",
        "value": "Europe/Tallinn"
      },
      {
        "label": "Europe/Uzhgorod",
        "value": "Europe/Uzhgorod"
      },
      {
        "label": "Europe/Vilnius",
        "value": "Europe/Vilnius"
      },
      {
        "label": "Europe/Zaporozhye",
        "value": "Europe/Zaporozhye"
      }
    ]
  },
  {
    "label": "Turkey Standard Time",
    "text": "(UTC+03:00) Istanbul",
    "offset": 3,
    "abbr": "TDT",
    "items": [
      {
        "label": "Europe/Istanbul",
        "value": "Europe/Istanbul"
      }
    ]
  },
  {
    "label": "Israel Standard Time",
    "text": "(UTC+02:00) Jerusalem",
    "offset": 3,
    "abbr": "JDT",
    "items": [
      {
        "label": "Asia/Jerusalem",
        "value": "Asia/Jerusalem"
      }
    ]
  },
  {
    "label": "Libya Standard Time",
    "text": "(UTC+02:00) Tripoli",
    "offset": 2,
    "abbr": "LST",
    "items": [
      {
        "label": "Africa/Tripoli",
        "value": "Africa/Tripoli"
      }
    ]
  },
  {
    "label": "Jordan Standard Time",
    "text": "(UTC+03:00) Amman",
    "offset": 3,
    "abbr": "JST",
    "items": [
      {
        "label": "Asia/Amman",
        "value": "Asia/Amman"
      }
    ]
  },
  {
    "label": "Arabic Standard Time",
    "text": "(UTC+03:00) Baghdad",
    "offset": 3,
    "abbr": "AST",
    "items": [
      {
        "label": "Asia/Baghdad",
        "value": "Asia/Baghdad"
      }
    ]
  },
  {
    "label": "Kaliningrad Standard Time",
    "text": "(UTC+02:00) Kaliningrad",
    "offset": 3,
    "abbr": "KST",
    "items": [
      {
        "label": "Europe/Kaliningrad",
        "value": "Europe/Kaliningrad"
      }
    ]
  },
  {
    "label": "Arab Standard Time",
    "text": "(UTC+03:00) Kuwait, Riyadh",
    "offset": 3,
    "abbr": "AST",
    "items": [
      {
        "label": "Asia/Aden",
        "value": "Asia/Aden"
      },
      {
        "label": "Asia/Bahrain",
        "value": "Asia/Bahrain"
      },
      {
        "label": "Asia/Kuwait",
        "value": "Asia/Kuwait"
      },
      {
        "label": "Asia/Qatar",
        "value": "Asia/Qatar"
      },
      {
        "label": "Asia/Riyadh",
        "value": "Asia/Riyadh"
      }
    ]
  },
  {
    "label": "E. Africa Standard Time",
    "text": "(UTC+03:00) Nairobi",
    "offset": 3,
    "abbr": "EAST",
    "items": [
      {
        "label": "Africa/Addis_Ababa",
        "value": "Africa/Addis_Ababa"
      },
      {
        "label": "Africa/Asmera",
        "value": "Africa/Asmera"
      },
      {
        "label": "Africa/Dar_es_Salaam",
        "value": "Africa/Dar_es_Salaam"
      },
      {
        "label": "Africa/Djibouti",
        "value": "Africa/Djibouti"
      },
      {
        "label": "Africa/Juba",
        "value": "Africa/Juba"
      },
      {
        "label": "Africa/Kampala",
        "value": "Africa/Kampala"
      },
      {
        "label": "Africa/Khartoum",
        "value": "Africa/Khartoum"
      },
      {
        "label": "Africa/Mogadishu",
        "value": "Africa/Mogadishu"
      },
      {
        "label": "Africa/Nairobi",
        "value": "Africa/Nairobi"
      },
      {
        "label": "Antarctica/Syowa",
        "value": "Antarctica/Syowa"
      },
      {
        "label": "Etc/GMT-3",
        "value": "Etc/GMT-3"
      },
      {
        "label": "Indian/Antananarivo",
        "value": "Indian/Antananarivo"
      },
      {
        "label": "Indian/Comoro",
        "value": "Indian/Comoro"
      },
      {
        "label": "Indian/Mayotte",
        "value": "Indian/Mayotte"
      }
    ]
  },
  {
    "label": "Moscow Standard Time",
    "text": "(UTC+03:00) Moscow, St. Petersburg, Volgograd, Minsk",
    "offset": 3,
    "abbr": "MSK",
    "items": [
      {
        "label": "Europe/Kirov",
        "value": "Europe/Kirov"
      },
      {
        "label": "Europe/Moscow",
        "value": "Europe/Moscow"
      },
      {
        "label": "Europe/Simferopol",
        "value": "Europe/Simferopol"
      },
      {
        "label": "Europe/Volgograd",
        "value": "Europe/Volgograd"
      },
      {
        "label": "Europe/Minsk",
        "value": "Europe/Minsk"
      }
    ]
  },
  {
    "label": "Samara Time",
    "text": "(UTC+04:00) Samara, Ulyanovsk, Saratov",
    "offset": 4,
    "abbr": "SAMT",
    "items": [
      {
        "label": "Europe/Astrakhan",
        "value": "Europe/Astrakhan"
      },
      {
        "label": "Europe/Samara",
        "value": "Europe/Samara"
      },
      {
        "label": "Europe/Ulyanovsk",
        "value": "Europe/Ulyanovsk"
      }
    ]
  },
  {
    "label": "Iran Standard Time",
    "text": "(UTC+03:30) Tehran",
    "offset": 4.5,
    "abbr": "IDT",
    "items": [
      {
        "label": "Asia/Tehran",
        "value": "Asia/Tehran"
      }
    ]
  },
  {
    "label": "Arabian Standard Time",
    "text": "(UTC+04:00) Abu Dhabi, Muscat",
    "offset": 4,
    "abbr": "AST",
    "items": [
      {
        "label": "Asia/Dubai",
        "value": "Asia/Dubai"
      },
      {
        "label": "Asia/Muscat",
        "value": "Asia/Muscat"
      },
      {
        "label": "Etc/GMT-4",
        "value": "Etc/GMT-4"
      }
    ]
  },
  {
    "label": "Azerbaijan Standard Time",
    "text": "(UTC+04:00) Baku",
    "offset": 5,
    "abbr": "ADT",
    "items": [
      {
        "label": "Asia/Baku",
        "value": "Asia/Baku"
      }
    ]
  },
  {
    "label": "Mauritius Standard Time",
    "text": "(UTC+04:00) Port Louis",
    "offset": 4,
    "abbr": "MST",
    "items": [
      {
        "label": "Indian/Mahe",
        "value": "Indian/Mahe"
      },
      {
        "label": "Indian/Mauritius",
        "value": "Indian/Mauritius"
      },
      {
        "label": "Indian/Reunion",
        "value": "Indian/Reunion"
      }
    ]
  },
  {
    "label": "Georgian Standard Time",
    "text": "(UTC+04:00) Tbilisi",
    "offset": 4,
    "abbr": "GET",
    "items": [
      {
        "label": "Asia/Tbilisi",
        "value": "Asia/Tbilisi"
      }
    ]
  },
  {
    "label": "Caucasus Standard Time",
    "text": "(UTC+04:00) Yerevan",
    "offset": 4,
    "abbr": "CST",
    "items": [
      {
        "label": "Asia/Yerevan",
        "value": "Asia/Yerevan"
      }
    ]
  },
  {
    "label": "Afghanistan Standard Time",
    "text": "(UTC+04:30) Kabul",
    "offset": 4.5,
    "abbr": "AST",
    "items": [
      {
        "label": "Asia/Kabul",
        "value": "Asia/Kabul"
      }
    ]
  },
  {
    "label": "West Asia Standard Time",
    "text": "(UTC+05:00) Ashgabat, Tashkent",
    "offset": 5,
    "abbr": "WAST",
    "items": [
      {
        "label": "Antarctica/Mawson",
        "value": "Antarctica/Mawson"
      },
      {
        "label": "Asia/Aqtau",
        "value": "Asia/Aqtau"
      },
      {
        "label": "Asia/Aqtobe",
        "value": "Asia/Aqtobe"
      },
      {
        "label": "Asia/Ashgabat",
        "value": "Asia/Ashgabat"
      },
      {
        "label": "Asia/Dushanbe",
        "value": "Asia/Dushanbe"
      },
      {
        "label": "Asia/Oral",
        "value": "Asia/Oral"
      },
      {
        "label": "Asia/Samarkand",
        "value": "Asia/Samarkand"
      },
      {
        "label": "Asia/Tashkent",
        "value": "Asia/Tashkent"
      },
      {
        "label": "Etc/GMT-5",
        "value": "Etc/GMT-5"
      },
      {
        "label": "Indian/Kerguelen",
        "value": "Indian/Kerguelen"
      },
      {
        "label": "Indian/Maldives",
        "value": "Indian/Maldives"
      }
    ]
  },
  {
    "label": "Yekaterinburg Time",
    "text": "(UTC+05:00) Yekaterinburg",
    "offset": 5,
    "abbr": "YEKT",
    "items": [
      {
        "label": "Asia/Yekaterinburg",
        "value": "Asia/Yekaterinburg"
      }
    ]
  },
  {
    "label": "Pakistan Standard Time",
    "text": "(UTC+05:00) Islamabad, Karachi",
    "offset": 5,
    "abbr": "PKT",
    "items": [
      {
        "label": "Asia/Karachi",
        "value": "Asia/Karachi"
      }
    ]
  },
  {
    "label": "India Standard Time",
    "text": "(UTC+05:30) Chennai, Kolkata, Mumbai, New Delhi",
    "offset": 5.5,
    "abbr": "IST",
    "items": [
      {
        "label": "Asia/Kolkata",
        "value": "Asia/Kolkata"
      },
      {
        "label": "Asia/Calcutta",
        "value": "Asia/Calcutta"
      }
    ]
  },
  {
    "label": "Sri Lanka Standard Time",
    "text": "(UTC+05:30) Sri Jayawardenepura",
    "offset": 5.5,
    "abbr": "SLST",
    "items": [
      {
        "label": "Asia/Colombo",
        "value": "Asia/Colombo"
      }
    ]
  },
  {
    "label": "Nepal Standard Time",
    "text": "(UTC+05:45) Kathmandu",
    "offset": 5.75,
    "abbr": "NST",
    "items": [
      {
        "label": "Asia/Kathmandu",
        "value": "Asia/Kathmandu"
      }
    ]
  },
  {
    "label": "Central Asia Standard Time",
    "text": "(UTC+06:00) Nur-Sultan (Astana)",
    "offset": 6,
    "abbr": "CAST",
    "items": [
      {
        "label": "Antarctica/Vostok",
        "value": "Antarctica/Vostok"
      },
      {
        "label": "Asia/Almaty",
        "value": "Asia/Almaty"
      },
      {
        "label": "Asia/Bishkek",
        "value": "Asia/Bishkek"
      },
      {
        "label": "Asia/Qyzylorda",
        "value": "Asia/Qyzylorda"
      },
      {
        "label": "Asia/Urumqi",
        "value": "Asia/Urumqi"
      },
      {
        "label": "Etc/GMT-6",
        "value": "Etc/GMT-6"
      },
      {
        "label": "Indian/Chagos",
        "value": "Indian/Chagos"
      }
    ]
  },
  {
    "label": "Bangladesh Standard Time",
    "text": "(UTC+06:00) Dhaka",
    "offset": 6,
    "abbr": "BST",
    "items": [
      {
        "label": "Asia/Dhaka",
        "value": "Asia/Dhaka"
      },
      {
        "label": "Asia/Thimphu",
        "value": "Asia/Thimphu"
      }
    ]
  },
  {
    "label": "Myanmar Standard Time",
    "text": "(UTC+06:30) Yangon (Rangoon)",
    "offset": 6.5,
    "abbr": "MST",
    "items": [
      {
        "label": "Asia/Rangoon",
        "value": "Asia/Rangoon"
      },
      {
        "label": "Indian/Cocos",
        "value": "Indian/Cocos"
      }
    ]
  },
  {
    "label": "SE Asia Standard Time",
    "text": "(UTC+07:00) Bangkok, Hanoi, Jakarta",
    "offset": 7,
    "abbr": "SAST",
    "items": [
      {
        "label": "Antarctica/Davis",
        "value": "Antarctica/Davis"
      },
      {
        "label": "Asia/Bangkok",
        "value": "Asia/Bangkok"
      },
      {
        "label": "Asia/Hovd",
        "value": "Asia/Hovd"
      },
      {
        "label": "Asia/Jakarta",
        "value": "Asia/Jakarta"
      },
      {
        "label": "Asia/Phnom_Penh",
        "value": "Asia/Phnom_Penh"
      },
      {
        "label": "Asia/Pontianak",
        "value": "Asia/Pontianak"
      },
      {
        "label": "Asia/Saigon",
        "value": "Asia/Saigon"
      },
      {
        "label": "Asia/Vientiane",
        "value": "Asia/Vientiane"
      },
      {
        "label": "Etc/GMT-7",
        "value": "Etc/GMT-7"
      },
      {
        "label": "Indian/Christmas",
        "value": "Indian/Christmas"
      }
    ]
  },
  {
    "label": "N. Central Asia Standard Time",
    "text": "(UTC+07:00) Novosibirsk",
    "offset": 7,
    "abbr": "NCAST",
    "items": [
      {
        "label": "Asia/Novokuznetsk",
        "value": "Asia/Novokuznetsk"
      },
      {
        "label": "Asia/Novosibirsk",
        "value": "Asia/Novosibirsk"
      },
      {
        "label": "Asia/Omsk",
        "value": "Asia/Omsk"
      }
    ]
  },
  {
    "label": "China Standard Time",
    "text": "(UTC+08:00) Beijing, Chongqing, Hong Kong, Urumqi",
    "offset": 8,
    "abbr": "CST",
    "items": [
      {
        "label": "Asia/Hong_Kong",
        "value": "Asia/Hong_Kong"
      },
      {
        "label": "Asia/Macau",
        "value": "Asia/Macau"
      },
      {
        "label": "Asia/Shanghai",
        "value": "Asia/Shanghai"
      }
    ]
  },
  {
    "label": "North Asia Standard Time",
    "text": "(UTC+08:00) Krasnoyarsk",
    "offset": 8,
    "abbr": "NAST",
    "items": [
      {
        "label": "Asia/Krasnoyarsk",
        "value": "Asia/Krasnoyarsk"
      }
    ]
  },
  {
    "label": "Singapore Standard Time",
    "text": "(UTC+08:00) Kuala Lumpur, Singapore",
    "offset": 8,
    "abbr": "MPST",
    "items": [
      {
        "label": "Asia/Brunei",
        "value": "Asia/Brunei"
      },
      {
        "label": "Asia/Kuala_Lumpur",
        "value": "Asia/Kuala_Lumpur"
      },
      {
        "label": "Asia/Kuching",
        "value": "Asia/Kuching"
      },
      {
        "label": "Asia/Makassar",
        "value": "Asia/Makassar"
      },
      {
        "label": "Asia/Manila",
        "value": "Asia/Manila"
      },
      {
        "label": "Asia/Singapore",
        "value": "Asia/Singapore"
      },
      {
        "label": "Etc/GMT-8",
        "value": "Etc/GMT-8"
      }
    ]
  },
  {
    "label": "W. Australia Standard Time",
    "text": "(UTC+08:00) Perth",
    "offset": 8,
    "abbr": "WAST",
    "items": [
      {
        "label": "Antarctica/Casey",
        "value": "Antarctica/Casey"
      },
      {
        "label": "Australia/Perth",
        "value": "Australia/Perth"
      }
    ]
  },
  {
    "label": "Taipei Standard Time",
    "text": "(UTC+08:00) Taipei",
    "offset": 8,
    "abbr": "TST",
    "items": [
      {
        "label": "Asia/Taipei",
        "value": "Asia/Taipei"
      }
    ]
  },
  {
    "label": "Ulaanbaatar Standard Time",
    "text": "(UTC+08:00) Ulaanbaatar",
    "offset": 8,
    "abbr": "UST",
    "items": [
      {
        "label": "Asia/Choibalsan",
        "value": "Asia/Choibalsan"
      },
      {
        "label": "Asia/Ulaanbaatar",
        "value": "Asia/Ulaanbaatar"
      }
    ]
  },
  {
    "label": "North Asia East Standard Time",
    "text": "(UTC+08:00) Irkutsk",
    "offset": 8,
    "abbr": "NAEST",
    "items": [
      {
        "label": "Asia/Irkutsk",
        "value": "Asia/Irkutsk"
      }
    ]
  },
  {
    "label": "Japan Standard Time",
    "text": "(UTC+09:00) Osaka, Sapporo, Tokyo",
    "offset": 9,
    "abbr": "JST",
    "items": [
      {
        "label": "Asia/Dili",
        "value": "Asia/Dili"
      },
      {
        "label": "Asia/Jayapura",
        "value": "Asia/Jayapura"
      },
      {
        "label": "Asia/Tokyo",
        "value": "Asia/Tokyo"
      },
      {
        "label": "Etc/GMT-9",
        "value": "Etc/GMT-9"
      },
      {
        "label": "Pacific/Palau",
        "value": "Pacific/Palau"
      }
    ]
  },
  {
    "label": "Korea Standard Time",
    "text": "(UTC+09:00) Seoul",
    "offset": 9,
    "abbr": "KST",
    "items": [
      {
        "label": "Asia/Pyongyang",
        "value": "Asia/Pyongyang"
      },
      {
        "label": "Asia/Seoul",
        "value": "Asia/Seoul"
      }
    ]
  },
  {
    "label": "Cen. Australia Standard Time",
    "text": "(UTC+09:30) Adelaide",
    "offset": 9.5,
    "abbr": "CAST",
    "items": [
      {
        "label": "Australia/Adelaide",
        "value": "Australia/Adelaide"
      },
      {
        "label": "Australia/Broken_Hill",
        "value": "Australia/Broken_Hill"
      }
    ]
  },
  {
    "label": "AUS Central Standard Time",
    "text": "(UTC+09:30) Darwin",
    "offset": 9.5,
    "abbr": "ACST",
    "items": [
      {
        "label": "Australia/Darwin",
        "value": "Australia/Darwin"
      }
    ]
  },
  {
    "label": "E. Australia Standard Time",
    "text": "(UTC+10:00) Brisbane",
    "offset": 10,
    "abbr": "EAST",
    "items": [
      {
        "label": "Australia/Brisbane",
        "value": "Australia/Brisbane"
      },
      {
        "label": "Australia/Lindeman",
        "value": "Australia/Lindeman"
      }
    ]
  },
  {
    "label": "AUS Eastern Standard Time",
    "text": "(UTC+10:00) Canberra, Melbourne, Sydney",
    "offset": 10,
    "abbr": "AEST",
    "items": [
      {
        "label": "Australia/Melbourne",
        "value": "Australia/Melbourne"
      },
      {
        "label": "Australia/Sydney",
        "value": "Australia/Sydney"
      }
    ]
  },
  {
    "label": "West Pacific Standard Time",
    "text": "(UTC+10:00) Guam, Port Moresby",
    "offset": 10,
    "abbr": "WPST",
    "items": [
      {
        "label": "Antarctica/DumontDUrville",
        "value": "Antarctica/DumontDUrville"
      },
      {
        "label": "Etc/GMT-10",
        "value": "Etc/GMT-10"
      },
      {
        "label": "Pacific/Guam",
        "value": "Pacific/Guam"
      },
      {
        "label": "Pacific/Port_Moresby",
        "value": "Pacific/Port_Moresby"
      },
      {
        "label": "Pacific/Saipan",
        "value": "Pacific/Saipan"
      },
      {
        "label": "Pacific/Truk",
        "value": "Pacific/Truk"
      }
    ]
  },
  {
    "label": "Tasmania Standard Time",
    "text": "(UTC+10:00) Hobart",
    "offset": 10,
    "abbr": "TST",
    "items": [
      {
        "label": "Australia/Currie",
        "value": "Australia/Currie"
      },
      {
        "label": "Australia/Hobart",
        "value": "Australia/Hobart"
      }
    ]
  },
  {
    "label": "Yakutsk Standard Time",
    "text": "(UTC+09:00) Yakutsk",
    "offset": 9,
    "abbr": "YST",
    "items": [
      {
        "label": "Asia/Chita",
        "value": "Asia/Chita"
      },
      {
        "label": "Asia/Khandyga",
        "value": "Asia/Khandyga"
      },
      {
        "label": "Asia/Yakutsk",
        "value": "Asia/Yakutsk"
      }
    ]
  },
  {
    "label": "Central Pacific Standard Time",
    "text": "(UTC+11:00) Solomon Is., New Caledonia",
    "offset": 11,
    "abbr": "CPST",
    "items": [
      {
        "label": "Antarctica/Macquarie",
        "value": "Antarctica/Macquarie"
      },
      {
        "label": "Etc/GMT-11",
        "value": "Etc/GMT-11"
      },
      {
        "label": "Pacific/Efate",
        "value": "Pacific/Efate"
      },
      {
        "label": "Pacific/Guadalcanal",
        "value": "Pacific/Guadalcanal"
      },
      {
        "label": "Pacific/Kosrae",
        "value": "Pacific/Kosrae"
      },
      {
        "label": "Pacific/Noumea",
        "value": "Pacific/Noumea"
      },
      {
        "label": "Pacific/Ponape",
        "value": "Pacific/Ponape"
      }
    ]
  },
  {
    "label": "Vladivostok Standard Time",
    "text": "(UTC+11:00) Vladivostok",
    "offset": 11,
    "abbr": "VST",
    "items": [
      {
        "label": "Asia/Sakhalin",
        "value": "Asia/Sakhalin"
      },
      {
        "label": "Asia/Ust-Nera",
        "value": "Asia/Ust-Nera"
      },
      {
        "label": "Asia/Vladivostok",
        "value": "Asia/Vladivostok"
      }
    ]
  },
  {
    "label": "New Zealand Standard Time",
    "text": "(UTC+12:00) Auckland, Wellington",
    "offset": 12,
    "abbr": "NZST",
    "items": [
      {
        "label": "Antarctica/McMurdo",
        "value": "Antarctica/McMurdo"
      },
      {
        "label": "Pacific/Auckland",
        "value": "Pacific/Auckland"
      }
    ]
  },
  {
    "label": "UTC+12",
    "text": "(UTC+12:00) Coordinated Universal Time+12",
    "offset": 12,
    "abbr": "U",
    "items": [
      {
        "label": "Etc/GMT-12",
        "value": "Etc/GMT-12"
      },
      {
        "label": "Pacific/Funafuti",
        "value": "Pacific/Funafuti"
      },
      {
        "label": "Pacific/Kwajalein",
        "value": "Pacific/Kwajalein"
      },
      {
        "label": "Pacific/Majuro",
        "value": "Pacific/Majuro"
      },
      {
        "label": "Pacific/Nauru",
        "value": "Pacific/Nauru"
      },
      {
        "label": "Pacific/Tarawa",
        "value": "Pacific/Tarawa"
      },
      {
        "label": "Pacific/Wake",
        "value": "Pacific/Wake"
      },
      {
        "label": "Pacific/Wallis",
        "value": "Pacific/Wallis"
      }
    ]
  },
  {
    "label": "Fiji Standard Time",
    "text": "(UTC+12:00) Fiji",
    "offset": 12,
    "abbr": "FST",
    "items": [
      {
        "label": "Pacific/Fiji",
        "value": "Pacific/Fiji"
      }
    ]
  },
  {
    "label": "Magadan Standard Time",
    "text": "(UTC+12:00) Magadan",
    "offset": 12,
    "abbr": "MST",
    "items": [
      {
        "label": "Asia/Anadyr",
        "value": "Asia/Anadyr"
      },
      {
        "label": "Asia/Kamchatka",
        "value": "Asia/Kamchatka"
      },
      {
        "label": "Asia/Magadan",
        "value": "Asia/Magadan"
      },
      {
        "label": "Asia/Srednekolymsk",
        "value": "Asia/Srednekolymsk"
      }
    ]
  },
  {
    "label": "Kamchatka Standard Time",
    "text": "(UTC+12:00) Petropavlovsk-Kamchatsky - Old",
    "offset": 13,
    "abbr": "KDT",
    "items": [
      {
        "label": "Asia/Kamchatka",
        "value": "Asia/Kamchatka"
      }
    ]
  },
  {
    "label": "Tonga Standard Time",
    "text": "(UTC+13:00) Nuku'alofa",
    "offset": 13,
    "abbr": "TST",
    "items": [
      {
        "label": "Etc/GMT-13",
        "value": "Etc/GMT-13"
      },
      {
        "label": "Pacific/Enderbury",
        "value": "Pacific/Enderbury"
      },
      {
        "label": "Pacific/Fakaofo",
        "value": "Pacific/Fakaofo"
      },
      {
        "label": "Pacific/Tongatapu",
        "value": "Pacific/Tongatapu"
      }
    ]
  },
  {
    "label": "Samoa Standard Time",
    "text": "(UTC+13:00) Samoa",
    "offset": 13,
    "abbr": "SST",
    "items": [
      {
        "label": "Pacific/Apia",
        "value": "Pacific/Apia"
      }
    ]
  }
]

const filteredTimezones = ref([])
const search = (event) => {
  let query = event.query;
  let newFilteredTimezones = [];

  for (let timezone of timezones) {
    let filteredItems = FilterService.filter(timezone.items, ['label'], query, FilterMatchMode.CONTAINS);
    if (filteredItems && filteredItems.length) {
      newFilteredTimezones.push({...timezone, ...{items: filteredItems}});
    }
  }

  filteredTimezones.value = newFilteredTimezones;
}

useSeoMeta({
  title: 'Timezone Converter',
  ogTitle: 'Timezone Converter',
  description: 'Timezone Converter',
  ogDescription: 'Timezone Converter',
  ogImage: '',
})
</script>

<template>
  <div class="grid">
    <div class="col-12">
      <div class="card">
        <h1>Timezone Converter</h1>
        <p>Convert time from one timezone to another</p>

        <div class="grid">
          <div class="col-12 md:col-6">
            <div class="p-inputgroup flex-1">
              <span class="p-inputgroup-addon">
               Input Time
             </span>
              <Calendar v-model="inputTime" time-only hour-format="12" placeholder="Input time"/>
              <AutoComplete v-model="inputTimezone" :suggestions="filteredTimezones" @complete="search"
                            option-label="label" optionGroupLabel="label" optionGroupChildren="items"
                            force-selection
                            placeholder="Search timezone"/>

            </div>
          </div>
          <div class="col-12 md:col-6">
            <div class="p-inputgroup flex-1">
              <span class="p-inputgroup-addon">
                Output Time
              </span>
              <Calendar :model-value="outputTime" readonly time-only hour-format="12" placeholder="Output time"/>
              <AutoComplete v-model="outputTimezone" :suggestions="filteredTimezones" @complete="search"
                            option-label="label" optionGroupLabel="label" optionGroupChildren="items"
                            force-selection
                            placeholder="Search timezone"/>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped lang="scss">

</style>