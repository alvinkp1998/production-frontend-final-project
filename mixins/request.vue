<script>
export default {
  methods: {
    confirm(message) {
      return this.$swal({
        icon: "question",
        title: "Are you sure?",
        text: message,
        showCancelButton: true
      });
    },
    async requestGet(url) {
      try {
        const data = await this.$axios.$get(url);
        return data;
      } catch (error) {
        this.$swal({
          icon: "warning",
          title: "Gagal Memuat Kelas!",
          text: error.toString()
        });
      }
    },
    async requestDelete(url) {
      try {
        const data = await this.$axios.$delete(url);
        this.$swal({
          icon: "success",
          title: "Good!!!",
          text: "data berhasil dihapus"
        });
        return data;
      } catch (error) {
        this.$swal({
          icon: "warning",
          title: "Bahaya!!!",
          text: error.toString()
        });
      }
    }
  }
};
</script>
