<template>
  <div class="container">
    <h4>Tutor & SPV</h4>
    <hr />
    <div class="row">
      <div
        class="col-sm-4 col-md-3 col-6"
        v-for="(tutorspv, i) in tutorspvs"
        :key="i"
      >
        <anggota
          :nama="tutorspv.nama"
          :role="tutorspv.role"
          :img="tutorspv.img"
        />
      </div>
    </div>

    <h4>Student</h4>
    <hr />
    <div class="row">
      <div
        class="col-sm-4 col-md-3 col-6"
        v-for="(student, i) in students"
        :key="i"
      >
        <anggota :nama="student.nama" :role="student.role" :img="student.img" />
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      tutorspvs: [
        {
          nama: "Ghany Ersa Abdillah",
          role: "Tutor",
          img:
            "https://cdnt.orami.co.id/unsafe/468x288/cdn-cas.orami.co.id/parenting/images/gong_yoo_korea.width-800.jpg"
        },
        {
          nama: "Atika Rahmawati",
          role: "SPV",
          img:
            "https://asset.kompas.com/crops/qEzp1lRjF_h3AOjVv8rhNwzoomU=/0x500:1000x1167/750x500/data/photo/2018/08/19/2853283469.jpg"
        }
      ],
      students: [
        {
          nama: "Alvin Kusuma Putra",
          role: "Student",
          img:
            "https://cdn06.pramborsfm.com/storage/app/media/Prambors/Editorial/JI%20CHANG%20WOOK-20210726122921.jpg?tr=w-800"
        },
        {
          nama: "Alvin Kusuma Putra",
          role: "Student",
          img:
            "https://cdn06.pramborsfm.com/storage/app/media/Prambors/Editorial/JI%20CHANG%20WOOK-20210726122921.jpg?tr=w-800"
        },
        {
          nama: "Alvin Kusuma Putra",
          role: "Student",
          img:
            "https://cdn06.pramborsfm.com/storage/app/media/Prambors/Editorial/JI%20CHANG%20WOOK-20210726122921.jpg?tr=w-800"
        },
        {
          nama: "Alvin Kusuma Putra",
          role: "Student",
          img:
            "https://cdn06.pramborsfm.com/storage/app/media/Prambors/Editorial/JI%20CHANG%20WOOK-20210726122921.jpg?tr=w-800"
        },
        {
          nama: "Alvin Kusuma Putra",
          role: "Student",
          img:
            "https://cdn06.pramborsfm.com/storage/app/media/Prambors/Editorial/JI%20CHANG%20WOOK-20210726122921.jpg?tr=w-800"
        },
        {
          nama: "Alvin Kusuma Putra",
          role: "Student",
          img:
            "https://cdn06.pramborsfm.com/storage/app/media/Prambors/Editorial/JI%20CHANG%20WOOK-20210726122921.jpg?tr=w-800"
        },
        {
          nama: "Alvin Kusuma Putra",
          role: "Student",
          img:
            "https://cdn06.pramborsfm.com/storage/app/media/Prambors/Editorial/JI%20CHANG%20WOOK-20210726122921.jpg?tr=w-800"
        },
        {
          nama: "Alvin Kusuma Putra",
          role: "Student",
          img:
            "https://cdn06.pramborsfm.com/storage/app/media/Prambors/Editorial/JI%20CHANG%20WOOK-20210726122921.jpg?tr=w-800"
        }
      ]
    };
  }
};
</script>
