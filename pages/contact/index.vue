<template>
  <div>
    <UiNavLink :subject="subject" />
    <section>
      <UiPagetitle :subject="subject" :subheading="subheading" />
      <div class="l-container--small l-container--contents">
        <template v-if="submitted">
          <p class="c-text--pre" v-html="thanksText"></p>
          <NuxtLink to="/" class="c-button">トップページ</NuxtLink>
        </template>
        <template v-else>
          <div class="c-form-group">
            <p class="c-text c-text--pre">{{ response.details.inquiry_info }}</p>
            <p class="c-text--small">
              <span class="c-form-label__required">*</span>は必須項目です。
            </p>
          </div>
          <UiAlertError v-if="error" :error="error" />
          <form class="c-form">
            <div
              v-for="n in response.details.cols"
              :key="n.key"
              class="c-form-group"
            >
              <label :for="n.key" class="c-form-label">{{ n.title }}</label>
              <span v-if="n.required === 2" class="c-form-label__required"
                >*</span
              >
              <!-- テキスト -->
              <template v-if="n.type === 1">
                <input
                  v-model="submitData[n.key]"
                  :name="n.key"
                  :id="n.key"
                  type="text"
                />
              </template>
              <!--テキストエリア-->
              <template v-if="n.type === 2">
                <textarea
                  v-model="submitData[n.key]"
                  rows="4"
                  cols="60"
                  :name="n.key"
                  :id="n.key"
                  placeholder=""
                ></textarea>
              </template>
              <!--ラジオボタン-->
              <template v-if="n.type === 3">
                <ul>
                  <li v-for="option in n.options" :key="option.key">
                    <input
                      v-model="submitData[n.key]"
                      type="radio"
                      :name="n.key"
                      :value="option.key"
                      :id="n.key + '-' + option.key"
                      class="c-form-toggle__radio"
                    />
                    <label :for="n.key + '-' + option.key">
                      {{ option.value }}
                    </label>
                  </li>
                </ul>
              </template>
              <!--セレクトボックス-->
              <template v-if="n.type === 4">
                <select v-model="submitData[n.key]" :name="n.key" :id="n.key">
                  <option label="選択なし" value="">選択なし</option>
                  <option
                    v-for="option in n.options"
                    :key="option.key"
                    :label="option.value"
                    :value="option.key"
                  >
                    {{ option.value }}
                  </option>
                </select>
              </template>
              <!--チェックボックス-->
              <template v-if="n.type === 5">
                <ul>
                  <li v-for="option in n.options" :key="option.key">
                    <input
                      type="checkbox"
                      :name="n.key + '[]'"
                      :value="option.key"
                      :id="n.key + '-' + option.key"
                      v-model="submitData[n.key]"
                      class="c-form-toggle__checkbox"
                    />
                    <label :for="n.key + '-' + option.key">{{
                      option.value
                    }}</label>
                  </li>
                </ul>
              </template>
              <!--日付-->
              <template v-if="n.type === 6">
                <div class="u-display-flex u-display-flex-align-items-center">
                  <select
                    v-model="y"
                    @change="setYMD(n.key)"
                    :name="n.key + '_y'"
                    :id="n.key + '_y'"
                  >
                    <option label="選択なし" value="">選択なし</option>
                    <option
                      v-for="option in n.attribute.arrYear"
                      :key="option.key"
                      :label="option"
                      :value="option"
                    >
                      {{ option }}
                    </option></select
                  ><label :for="n.key + '_y'" class="u-pa-10">年</label>

                  <select
                    v-model="m"
                    @change="setYMD(n.key)"
                    :name="n.key + '_m'"
                  >
                    <option label="選択なし" value="">選択なし</option>
                    <option label="01" value="01">01</option>
                    <option label="02" value="02">02</option>
                    <option label="03" value="03">03</option>
                    <option label="04" value="04">04</option>
                    <option label="05" value="05">05</option>
                    <option label="06" value="06">06</option>
                    <option label="07" value="07">07</option>
                    <option label="08" value="08">08</option>
                    <option label="09" value="09">09</option>
                    <option label="10" value="10">10</option>
                    <option label="11" value="11">11</option>
                    <option label="12" value="12">12</option></select
                  ><label :for="n.key + '_m'" class="u-pa-10">月</label>
                  <select
                    v-model="d"
                    @change="setYMD(n.key)"
                    :name="n.key + '_d'"
                  >
                    <option label="選択なし" value="">選択なし</option>
                    <option label="01" value="01">01</option>
                    <option label="02" value="02">02</option>
                    <option label="03" value="03">03</option>
                    <option label="04" value="04">04</option>
                    <option label="05" value="05">05</option>
                    <option label="06" value="06">06</option>
                    <option label="07" value="07">07</option>
                    <option label="08" value="08">08</option>
                    <option label="09" value="09">09</option>
                    <option label="10" value="10">10</option>
                    <option label="11" value="11">11</option>
                    <option label="12" value="12">12</option>
                    <option label="13" value="13">13</option>
                    <option label="14" value="14">14</option>
                    <option label="15" value="15">15</option>
                    <option label="16" value="16">16</option>
                    <option label="17" value="17">17</option>
                    <option label="18" value="18">18</option>
                    <option label="19" value="19">19</option>
                    <option label="20" value="20">20</option>
                    <option label="21" value="21">21</option>
                    <option label="22" value="22">22</option>
                    <option label="23" value="23">23</option>
                    <option label="24" value="24">24</option>
                    <option label="25" value="25">25</option>
                    <option label="26" value="26">26</option>
                    <option label="27" value="27">27</option>
                    <option label="28" value="28">28</option>
                    <option label="29" value="29">29</option>
                    <option label="30" value="30">30</option>
                    <option label="31" value="31">31</option></select
                  ><label :for="n.key + '_d'" class="u-pa-10">日</label>
                </div>
              </template>
              <!--画像ファイル-->
              <template v-if="n.type === 7">
                <p></p>
                <p></p>
                <input
                  type="file"
                  :name="n.key"
                  :id="n.key"
                  @change="uploadFile($event, n.key)"
                />
              </template>
              <!--マトリックス(単一選択)-->
              <template
                v-if="n.type === 10 && n.attribute.selection_type === 'single'"
              >
                <table class="u-width-100">
                  <thead>
                    <tr>
                      <th></th>
                      <th
                        v-for="(options_col, i_col) in n.options[0].value"
                        :key="i_col"
                        scope="col"
                      >
                        {{ options_col }}
                      </th>
                    </tr>
                  </thead>
                  <tbody>
                    <tr
                      v-for="(options_row, i_row) in n.options[1].value"
                      :key="i_row"
                    >
                      <th scope="row">{{ options_row }}</th>
                      <td
                        v-for="(options_col, i_col) in n.options[0].value"
                        :key="i_col"
                        class="u-text-align-center"
                      >
                        <input
                          v-model="submitData[n.key][i_row - 1]"
                          type="radio"
                          :name="n.key + '[' + i_row + ']'"
                          :value="{
                            ROW: {
                              key: i_row,
                            },
                            COL: {
                              key: i_col,
                            },
                          }"
                        />
                      </td>
                    </tr>
                  </tbody>
                </table>
              </template>
              <!--マトリックス(複数選択)-->
              <template
                v-if="
                  n.type === 10 && n.attribute.selection_type === 'multiple'
                "
              >
                <table class="u-width-100">
                  <thead>
                    <tr>
                      <th></th>
                      <th
                        v-for="(options_col, i_col) in n.options[0].value"
                        :key="i_col"
                      >
                        {{ options_col }}
                      </th>
                    </tr>
                  </thead>
                  <tbody>
                    <tr
                      v-for="(options_row, i_row) in n.options[1].value"
                      :key="i_row"
                    >
                      <th>{{ options_row }}</th>
                      <td
                        v-for="(options_col, i_col) in n.options[0].value"
                        :key="i_col"
                        class="u-text-align-center"
                      >
                        <input
                          type="checkbox"
                          :id="i_col"
                          v-model="submitData[n.key][i_row - 1].COL"
                          :value="{
                            key: i_col,
                          }"
                          class="c-form-toggle__checkbox"
                        />
                      </td>
                    </tr>
                  </tbody>
                </table>
              </template>
            </div>

            <div class="c-form-group">
              <input
                type="checkbox"
                name=""
                value=""
                id="privacy"
                @click="disabled = !disabled"
              />
              <label for="privacy">
                <NuxtLink to="#">利用規約</NuxtLink>及び<NuxtLink to="/privacy/"
                  >プライバシーポリシー</NuxtLink
                >に同意する</label
              >
            </div>
            <button
              class="c-button--primary u-width-100"
              type="submit"
              id="inquiry_item_button_confirm"
              :disabled="disabled"
              @click.prevent="handleOnSubmit"
            >
              確認する
            </button>
          </form>
        </template>
      </div>
    </section>
  </div>
</template>

<script>
import AlertError from "../../components/ui/AlertError.vue";
export default {
  components: { AlertError },
  data() {
    return {
      submitted: false,
      submitData: {},
      error: null,
      file_id: null,
      y: null,
      m: null,
      d: null,
      disabled: true,
      thanksText: null,
      subject: "お問い合わせ",
      subheading: "Contact",
    };
  },
  async asyncData({ $axios }) {
    return {
      response: await $axios.$get("/rcms-api/1/inquiry/1"),
    };
  },
  created() {
    //配列形式が必要なタイプは事前に宣言
    Object.keys(this.response.details.cols).forEach((key) => {
      let object = this.response.details.cols[key];

      //複数選択チェックボックスとマトリックスは配列形式でセット
      if (object.type === 5 || object.type === 10) {
        this.$set(this.submitData, object.key, []);
      }

      //マトリックスの複数選択チェックボックスは列の数だけオブジェクトを追加し、"COL"は配列形式でセット
      if (
        object.type === 10 &&
        object.attribute.selection_type === "multiple"
      ) {
        Object.keys(object.options[1].value).forEach((key) => {
          this.submitData[object.key].push({
            ROW: {
              key: key,
            },
            COL: [],
          });
        });
      }
    });
  },
  methods: {
    //日付フォーマットのセット
    async setYMD(key) {
      this.$set(this.submitData, key, this.y + "-" + this.m + "-" + this.d);
    },
    //ファイルIDのセット
    async uploadFile(e, key) {
      const fm = new FormData();
      fm.append("file", e.target.files[0]);

      const { file_id } = await this.$axios.$post(`/rcms-api/1/upload`, fm, {
        headers: {
          "Content-Type": "multipart/form-data", // required to post file as a binary
        },
      });
      this.$set(this.submitData, key, {});
      this.$set(this.submitData[key], "file_id", file_id);
    },
    async handleOnSubmit() {
      try {
        const formresponse = await this.$axios.$post(
          "/rcms-api/1/inquiry/1",
          { ...this.submitData } // フォームの内容をリクエストボディとして適用
        );
        this.error = null;
        this.submitted = true;
        this.thanksText = formresponse.messages[0];
      } catch (e) {
        console.error(e);
        this.error = e.response.data.errors;
      }
    },
  },
};
</script>
