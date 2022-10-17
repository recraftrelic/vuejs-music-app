<template>
    <div v-if="!isPlayerVisible">
        <div class="text-yellow-300 font-bold text-center text-3xl mb-7 mt-3">
            BoudaCloud
        </div>
        <div
            v-for="(song, songIndex) in list" v-bind:key="song.id"
            class="flex flex-row justify-between mb-4 cursor-pointer"
            v-on:click="playSong(songIndex)"
        >
            <div>
                <span class="text-yellow-300">{{ song.name }}</span>
                <br />
                <span class="text-gray-200 text-xs">
                    {{ song.artistName }} - 
                    <span class="text-gray-400"> {{ song.albumName }} ({{ song.year }})</span>
                </span>
            </div>
            <div>
                <img
                    class="max-h-12 rounded"
                    v-bind:src="song.src"
                />
            </div>
        </div>
    </div>
    <div v-if="isPlayerVisible">
        <SongPlayer
            v-bind:song="list[currentSongIndex]"
            @goback="isPlayerVisible = !isPlayerVisible"
            @next="playNext"
            @previous="playPrevious"
        />
    </div>
</template>

<script>
import SongPlayer from './SongPlayer.vue';

export default {
    data () {
        return {
            isPlayerVisible: false,
            currentSongIndex: 0,
            list: [
  {
    "id": 0,
    "name": "N3icho La Vida",
    "artistName": "Cheb Momo",
    "year": 2020,
    "src": "https://raw.githubusercontent.com/DrissBouda/vuejs-music-app/master/src/assets/cheb momo.jpg",
    "songSrc": "http://xoom.virgilio.it/source_filemanager/ws/ss/wss/Cheb%20Momo%20-%20N3ichou%20la%20vida.mp3"
  },
  {
    "id": 1,
    "name": "Aghach",
    "artistName": "LFERDA",
    "year": 2020,
    "src": "https://raw.githubusercontent.com/DrissBouda/vuejs-music-app/master/src/assets/lferda.jpg",
    "songSrc": "http://xoom.virgilio.it/source_filemanager/ws/ss/wss/LFERDA%20-%20Aghach.mp3"
  },
  {
    "id": 2,
    "name": "Koula Nhar",
    "artistName": "Lord Mehdi",
    "year": 2020,
    "src": "https://raw.githubusercontent.com/DrissBouda/vuejs-music-app/master/src/assets/lord mehdi.jpg",
    "songSrc": "http://xoom.virgilio.it/source_filemanager/ws/ss/wss/Lord%20Mehdi%20-%20Koula%20Nhar.mp3"
  },
  {
    "id": 3,
    "name": "Tant pis",
    "artistName": "Lord Mehdi",
    "year": 2020,
    "src": "https://raw.githubusercontent.com/DrissBouda/vuejs-music-app/master/src/assets/lord mehdi.jpg",
    "songSrc": "http://xoom.virgilio.it/source_filemanager/ws/ss/wss/Lord%20Mehdi%20-%20Tant%20pis.mp3"
  },
  {
    "id": 4,
    "name": "Foutni W 9NI",
    "artistName": "Nessyou",
    "year": 2020,
    "src": "https://raw.githubusercontent.com/DrissBouda/vuejs-music-app/master/src/assets/nessyou.jpg",
    "songSrc": "http://xoom.virgilio.it/source_filemanager/ws/ss/wss/Nessyou%20-%20Foutni%20w%209ni.mp3"
  },
  {
    "id": 5,
    "name": "DRAIL",
    "artistName": "MA3iZ",
    "year": 2020,
    "src": "https://raw.githubusercontent.com/DrissBouda/vuejs-music-app/master/src/assets/ma3iz.jpg",
    "songSrc": "http://xoom.virgilio.it/source_filemanager/ws/ss/wss/MA3IZ%20-%20DRAILL.mp3"
  },
  {
    "id": 6,
    "name": "JRO7i",
    "artistName": "MA3iZ",
    "year": 2020,
    "src": "https://raw.githubusercontent.com/DrissBouda/vuejs-music-app/master/src/assets/ma3iz.jpg",
    "songSrc": "https://xoom.virgilio.it/source_filemanager/ws/ss/wss/MA3IZ%20-%20JRO7I.mp3"
  },
  {
    "id": 7,
    "name": "Adams Ft. Raid",
    "artistName": "Lmorphine",
    "year": 2020,
    "src": "https://raw.githubusercontent.com/DrissBouda/vuejs-music-app/master/src/assets/lmorphine.jpg",
    "songSrc": "https://wss.xoom.it/inkonnu/L%20morphine%20-%20Adams%2C%20Raid.mp3"
  },
  {
    "id": 8,
    "name": "Sparadra",
    "artistName": "Lmorphine",
    "year": 2020,
    "src": "https://raw.githubusercontent.com/DrissBouda/vuejs-music-app/master/src/assets/lmorphine.jpg",
    "songSrc": "http://xoom.virgilio.it/source_filemanager/ws/ss/wss/inkonnu/L%20morphine%20-%20Sparadra.mp3"
  },
  {
    "id": 9,
    "name": "Tab3ini V3",
    "artistName": "Inkonnu",
    "year": 2020,
    "src": "https://raw.githubusercontent.com/DrissBouda/vuejs-music-app/master/src/assets/inkonnu.jpg",
    "songSrc": "https://wss.xoom.it/inkonnu/Inkonnu%20-%20Tab3ini%20V3.mp3"
  },
  {
    "id": 10,
    "name": "RIP LOVE",
    "artistName": "Faouzia",
    "year": 2020,
    "src": "https://raw.githubusercontent.com/DrissBouda/vuejs-music-app/master/src/assets/faouzia.jpg",
    "songSrc": "http://xoom.virgilio.it/source_filemanager/ws/ss/wss/Faouzia%20-%20RIP%2C%20Love.mp3"
  },
  {
    "id": 11,
    "name": "Breda",
    "artistName": "Inkonnu",
    "year": 2020,
    "src": "https://raw.githubusercontent.com/DrissBouda/vuejs-music-app/master/src/assets/inkonnu.jpg",
    "songSrc": "https://xoom.virgilio.it/source_filemanager/ws/ss/wss/inkonnu/Inkonnu%20-%20BREDA.mp3"
  },
  {
    "id": 12,
    "name": "Chill",
    "artistName": "Inkonnu",
    "year": 2020,
    "src": "https://raw.githubusercontent.com/DrissBouda/vuejs-music-app/master/src/assets/inkonnu.jpg",
    "songSrc": "https://xoom.virgilio.it/source_filemanager/ws/ss/wss/inkonnu/Inkonnu%20-%20Chill.mp3"
  },
  {
    "id": 13,
    "name": "Matebkich",
    "artistName": "Klass-A",
    "year": 2020,
    "src": "https://raw.githubusercontent.com/DrissBouda/vuejs-music-app/master/src/assets/klass-a.jpg",
    "songSrc": "https://xoom.virgilio.it/source_filemanager/ws/ss/wss/inkonnu/Klass-A%20-%20Matebkich.mp3"
  },
  {
    "id": 14,
    "name": "After Prophets Life",
    "artistName": "Nostik",
    "year": 2020,
    "src": "https://raw.githubusercontent.com/DrissBouda/vuejs-music-app/master/src/assets/nostik.jpg",
    "songSrc": "https://xoom.virgilio.it/source_filemanager/ws/ss/wss/Nostik%20-%20After%20Prophets%20Life.mp3"
  },
  {
    "id": 15,
    "name": "Aladin",
    "artistName": "Nostik",
    "year": 2020,
    "src": "https://raw.githubusercontent.com/DrissBouda/vuejs-music-app/master/src/assets/nostik.jpg",
    "songSrc": "https://p52.f0.n0.cdn.getcloudapp.com/items/JruOYyXK/54cabd1f-ab5b-4c39-9c87-50f79f6ed34d.mp3"
  },
  {
    "id": 16,
    "name": "Lbaroud Ft. Inkonnu",
    "artistName": "Draganov",
    "year": 2020,
    "src": "https://raw.githubusercontent.com/DrissBouda/vuejs-music-app/master/src/assets/draganov.jpg",
    "songSrc": "https://p52.f0.n0.cdn.getcloudapp.com/items/kpun0qBY/a3256b56-a70d-4582-8ce7-be6201c7fb8f.mp3"
  },
  {
    "id": 17,
    "name": "Comite",
    "artistName": "Draganov",
    "year": 2020,
    "src": "https://raw.githubusercontent.com/DrissBouda/vuejs-music-app/master/src/assets/draganov.jpg",
    "songSrc": "https://p52.f0.n0.cdn.getcloudapp.com/items/qGuRjLAY/56cef9e1-f40c-4588-9595-884f26349103.mp3"
  },
  {
    "id": 18,
    "name": "Ma Cherie",
    "artistName": "Naika",
    "year": 2020,
    "src": "https://raw.githubusercontent.com/DrissBouda/vuejs-music-app/master/src/assets/naika.jpg",
    "songSrc": "https://p52.f0.n0.cdn.getcloudapp.com/items/DOu6XyDx/c5154877-3454-4e57-bd5b-cfe08bd322ac.mp3"
  },
  {
    "id": 19,
    "name": "Kssiriri",
    "artistName": "Draganov",
    "year": 2020,
    "src": "https://raw.githubusercontent.com/DrissBouda/vuejs-music-app/master/src/assets/draganov.jpg",
    "songSrc": "https://p52.f0.n0.cdn.getcloudapp.com/items/ApuEB2wO/c63faea2-a58e-46d5-b071-48d5432a8330.mp3"
  },
  {
    "id": 20,
    "name": "Table 42",
    "artistName": "Klass-A",
    "year": 2020,
    "src": "https://raw.githubusercontent.com/DrissBouda/vuejs-music-app/master/src/assets/klass-a.jpg",
    "songSrc": "https://p52.f0.n0.cdn.getcloudapp.com/items/geuA4Qn5/41f9c549-8c8e-4fee-895a-22f937ff021f.mp3"
  },
  {
    "id": 21,
    "name": "Cellule Ft. Raid",
    "artistName": "Diib",
    "year": 2020,
    "src": "https://raw.githubusercontent.com/DrissBouda/vuejs-music-app/master/src/assets/diib.jpg",
    "songSrc": "https://p52.f0.n0.cdn.getcloudapp.com/items/12uvoq58/5fe82507-0478-49b2-a194-9ad23494e9fc.mp3"
  },
  {
    "id": 22,
    "name": "Prince Nassim",
    "artistName": "Hamza15-3",
    "year": 2020,
    "src": "https://raw.githubusercontent.com/DrissBouda/vuejs-music-app/master/src/assets/hamza15-3.jpg",
    "songSrc": "https://p52.f0.n0.cdn.getcloudapp.com/items/Jrux1lQe/5db26c0a-470b-404d-a782-ce92d50265d6.mp3"
  },
  {
    "id": 23,
    "name": "Denya",
    "artistName": "Klass-A",
    "year": 2020,
    "src": "https://raw.githubusercontent.com/DrissBouda/vuejs-music-app/master/src/assets/klass-a.jpg",
    "songSrc": "https://p52.f0.n0.cdn.getcloudapp.com/items/P8uGY1g0/794bd993-b5d6-47a4-aebc-bfca989babe8.mp3"
  },
  {
    "id": 24,
    "name": "Flashback",
    "artistName": "Vargas",
    "year": 2020,
    "src": "https://raw.githubusercontent.com/DrissBouda/vuejs-music-app/master/src/assets/vargas.jpg",
    "songSrc": "https://p52.f0.n0.cdn.getcloudapp.com/items/d5uReANg/6e14fd57-bda4-48a2-abcb-9ab4fc5c962f.mp3"
  },
  {
    "id": 25,
    "name": "DNT Ft. Nouvo",
    "artistName": "Draganov",
    "year": 2020,
    "src": "https://raw.githubusercontent.com/DrissBouda/vuejs-music-app/master/src/assets/draganov.jpg",
    "songSrc": "https://p52.f0.n0.cdn.getcloudapp.com/items/lluojlA0/d5845ba6-ea54-4e5b-a296-f7983dae7329.flac"
  },
  {
    "id": 26,
    "name": "Youm Wara Youm",
    "artistName": "Stormy",
    "year": 2020,
    "src": "https://raw.githubusercontent.com/DrissBouda/vuejs-music-app/master/src/assets/stormy.jpg",
    "songSrc": "https://p52.f0.n0.cdn.getcloudapp.com/items/mXuKdXQp/74059561-128e-48e2-b5dc-cedb8a8a72d3.mp3"
  },
  {
    "id": 27,
    "name": "Hkaya",
    "artistName": "SNOR",
    "year": 2020,
    "src": "https://raw.githubusercontent.com/DrissBouda/vuejs-music-app/master/src/assets/snor.jpg",
    "songSrc": "https://p52.f0.n0.cdn.getcloudapp.com/items/L1uBA0L0/2c576c7f-ee26-4f58-84e5-b21c65fd7486.mp3"
  },
  {
    "id": 28,
    "name": "Bonne Année",
    "artistName": "Tawsen",
    "year": 2020,
    "src": "https://raw.githubusercontent.com/DrissBouda/vuejs-music-app/master/src/assets/tawsen.jpg",
    "songSrc": "https://p52.f0.n0.cdn.getcloudapp.com/items/z8uOgdmL/68bcc597-fe88-42f3-a63b-1ee1514fbd25.mp3"
  },
  {
    "id": 29,
    "name": "Omri Ana Ft. Tagne",
    "artistName": "Stormy",
    "year": 2020,
    "src": "https://raw.githubusercontent.com/DrissBouda/vuejs-music-app/master/src/assets/stormy.jpg",
    "songSrc": "https://p52.f0.n0.cdn.getcloudapp.com/items/JruDOE8X/2aff8d7b-1ed3-4fa3-a4c6-f6f7e4082ec6.mp3"
  },
  {
    "id": 30,
    "name": "Tri9 Lil Ft. Gha4",
    "artistName": "Inkonnu",
    "year": 2020,
    "src": "https://raw.githubusercontent.com/DrissBouda/vuejs-music-app/master/src/assets/inkonnu.jpg",
    "songSrc": "https://p52.f0.n0.cdn.getcloudapp.com/items/kpuDJZnE/c19ff085-c55b-4d8f-9889-f77f5a3e71ab.mp3"
  },
  {
    "id": 31,
    "name": "Shredder",
    "artistName": "Diib",
    "year": 2020,
    "src": "https://raw.githubusercontent.com/DrissBouda/vuejs-music-app/master/src/assets/diib.jpg",
    "songSrc": "https://p52.f0.n0.cdn.getcloudapp.com/items/rRujJ2on/16ba29e5-ae1d-4f6b-8847-a50a103ca49d.flac"
  },
  {
    "id": 32,
    "name": "N",
    "artistName": "Madd",
    "year": 2020,
    "src": "https://raw.githubusercontent.com/DrissBouda/vuejs-music-app/master/src/assets/madd.jpg",
    "songSrc": "https://p52.f0.n0.cdn.getcloudapp.com/items/wbu6j5D2/e11adcff-179e-4383-8f85-38248c234c53.mp3"
  },
  {
    "id": 33,
    "name": "Peek.A.Boo",
    "artistName": "Pause",
    "year": 2020,
    "src": "https://raw.githubusercontent.com/DrissBouda/vuejs-music-app/master/src/assets/pause.jpg",
    "songSrc": "https://p9.f1.n0.cdn.getcloudapp.com/items/Blu4nw8E/9e9b4361-46bc-46bf-9a7f-95aaf50cbd4b.mp3"
  },
  {
    "id": 34,
    "name": "Tt Va Bien",
    "artistName": "Draganov",
    "year": 2020,
    "src": "https://raw.githubusercontent.com/DrissBouda/vuejs-music-app/master/src/assets/draganov.jpg",
    "songSrc": "https://p52.f0.n0.cdn.getcloudapp.com/items/4gu2odqL/77c1ba15-fa28-47c7-a5e3-ab3972b8ac73.mp3"
  },
  {
    "id": 35,
    "name": "Memo",
    "artistName": "Furelise",
    "year": 2020,
    "src": "https://raw.githubusercontent.com/DrissBouda/vuejs-music-app/master/src/assets/furelise.jpg",
    "songSrc": "https://p52.f0.n0.cdn.getcloudapp.com/items/Z4uj6xk5/2e8ff242-7cfc-48f5-b9a5-83f5cd67d3a1.mp3"
  },
  {
    "id": 36,
    "name": "Lili",
    "artistName": "Plylist",
    "year": 2020,
    "src": "https://raw.githubusercontent.com/DrissBouda/vuejs-music-app/master/src/assets/plylist.jpg",
    "songSrc": "https://p9.f1.n0.cdn.getcloudapp.com/items/llu5WmNq/5955d479-c49f-45b5-bfc5-737214510edd.mp3"
  },
  {
    "id": 37,
    "name": "ALOHA",
    "artistName": "ElGrandeToto",
    "year": 2020,
    "src": "https://raw.githubusercontent.com/DrissBouda/vuejs-music-app/master/src/assets/elgrandetoto.jpg",
    "songSrc": "https://p52.f0.n0.cdn.getcloudapp.com/items/RBuYA5QP/e27eb3e0-13e8-4931-a2eb-a1d677aa186b.mp3"
  },
  {
    "id": 38,
    "name": "Morose",
    "artistName": "Damso",
    "year": 2020,
    "src": "https://raw.githubusercontent.com/DrissBouda/vuejs-music-app/master/src/assets/damso.jpg",
    "songSrc": "https://p52.f0.n0.cdn.getcloudapp.com/items/xQubRrx5/16a5093a-fda3-4559-a3ef-ea66f0a188fc.mp3"
  },
  {
    "id": 39,
    "name": "Pegasus Ft. Raid & Diib",
    "artistName": "Mehdi Black Wind",
    "year": 2020,
    "src": "https://raw.githubusercontent.com/DrissBouda/vuejs-music-app/master/src/assets/mehdi black wind.jpg",
    "songSrc": "https://drissbouda.xoom.it/mp3/Mehdi%20Black%20Wind%20-%20PEGASUS%20(feat.%20Diib%20&%20Raid).mp3"
  }
]
        }
    },
    methods: {
        playSong (index) {
            this.currentSongIndex = index;
            this.isPlayerVisible = true;
        },
        playNext () {
            if (this.currentSongIndex < this.list.length - 1) {
                this.currentSongIndex += 1;
            } else {
                this.currentSongIndex = 0;
            }
        },
        playPrevious () {
            if (this.currentSongIndex != 0) {
                this.currentSongIndex -= 1;
            } else {
                this.currentSongIndex = this.list.length - 1;
            }
        } 
    },
    components: {
        SongPlayer
    },
    name: 'SongList'
}
</script>
