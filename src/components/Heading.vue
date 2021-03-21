<script>
import { h } from "vue";
export default {
  props: {
    level: {
      default: 1
    }
  },

  setup({ level }, { slots }) {
    const slot = slots ? slots.default() : [];
    console.log(slot);
    const modifiedSlot = slot.map(({ children }) =>
      h("div", { style: "color:purple" }, children)
    );
    return () => h(`h${level}`, modifiedSlot);
  }
};
</script>

<style lang="scss" scoped></style>
