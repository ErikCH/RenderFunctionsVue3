<script>
import { h, ref } from "vue";
export default {
  setup(_, { slots }) {
    let inputValue = "";
    let shows = ref(null);
    let error = ref(null);

    const searchText = async (search) => {
      if (!search) return;
      shows.value = [];
      console.log("got here", search);

      const searchT = await fetch(
        `http://api.tvmaze.com/search/shows?q=${search}`
      ).catch((e) => {
        error.value = "error" + e;
        console.log("got error", error.value);
        return;
      });
      shows.value = await searchT?.json().catch((e) => (error.value = e));
      console.log(shows);
    };

    // 1. Create Basic Div
    // 2. create basic layout
    // map through data
    // click handlers
    // v-if error
    // default slots

    const slot = slots.default ? slots.default() : [];
    const namedSlot = slots.namedSlot ? slots.namedSlot() : [];

    const sc = (show) => (slots.sc ? slots.sc(show) : []);

    return () =>
      h(
        "form",
        {
          style: "color: red; max-width:768px; margin: auto",
          onSubmit: (event) => event.preventDefault()
        },
        [
          sc({ shows: shows.value }),
          namedSlot,
          slot,
          h("input", {
            onChange: (event) => {
              inputValue = event.target.value;
            }
          }),
          h(
            "button",
            {
              onClick: async () => {
                searchText(inputValue);
              }
            },
            "Press Me"
          ),
          h("div", { class: "shows" }, [
            error.value
              ? h("div", error.value)
              : shows.value?.map((show) =>
                  h("div", { class: "show" }, [
                    h("div", show.show.name),
                    h("img", { src: show.show.image?.medium })
                  ])
                )
          ])
        ]
      );
  }
};
</script>

<style>
.show {
  margin: 10px;
  min-width: 210px;
}
.shows {
  display: flex;
  flex-wrap: wrap;
  width: 100%;
  justify-content: center;
}
</style>
