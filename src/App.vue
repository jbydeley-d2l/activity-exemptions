<template>
  <div id="activity-exemptions">
    <button class="d2l-button primary" @click="setExempt">{{ $t('btnExempt') }}</button>
    <button class="d2l-button" @click="setUnexempt">{{ $t('btnUnexempt') }}</button>

    <p>
      {{ $t('lblExemptionCount', {exemptionCount}) }}
    </p>
    <table>
      <thead>
        <tr>
          <th>
            <input type="checkbox" class="d2l-checkbox" :checked="allSelected" @change="selectAll">
          </th>
          <th>{{ $t('lblLastFirstName') }}</th>
          <th>{{ $t('lblExemptStatus') }}</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="user in allUsers">
          <td>
            <input type="checkbox" class="d2l-checkbox" :checked="user.isSelected" @change="toggleSelection(user)">
          </td>
          <td>{{user.fullName}}</td>
          <td><span v-if="isUserExempt(user)">{{ $t('lblExempt') }}</span></td>
        </tr>
      </tbody>
    </table>
    <button class="d2l-button" v-if="hasMoreItems" @click="loadMore">{{ $t('btnLoadMore') }}</button>
    <button class="d2l-button primary" @click="setExempt">{{ $t('btnExempt') }}</button>
    <button class="d2l-button" @click="setUnexempt">{{ $t('btnUnexempt') }}</button>
  </div>
</template>

<script>
import { mapGetters, mapActions } from 'vuex';

export default {
  name: 'activity-exemptions',
  data() {
    return {
      locale: 'en'
    }
  },
  computed: {
    ...mapGetters(['allUsers', 'isUserExempt', 'exemptionCount', 'allSelected', 'hasMoreItems'])
  },
  methods: {
    ...mapActions(['toggleSelection', 'setExempt', 'setUnexempt', 'selectAll', 'loadMore'])
  }
}
</script>

<style scoped>

#activity-exemptions {
  color: #565a5c;
  font-family: 'Lato', 'Lucida Sans Unicode', 'Lucida Grande', sans-serif;
  padding-bottom: 50px;
}

table {
  background-color: transparent;
  border-collapse: separate !important;
  border-spacing: 0;
  display: table;
  font-size: 0.8rem;
  font-weight: 400;
  width: 100%;
}

thead {
  display: table-header-group;
}

thead tr:first-child {
  border-top: 1px solid #d3d9e3;
}

th {
  border-top: 1px solid #d3d9e3;
  color: #565a5c;
  background-color: #f9fafb;
  margin: 1rem 0;
  border-right: 1px solid #d3d9e3;
  padding: 1rem;
  text-align: left;
  vertical-align: middle;
}

th:first-child {
  border-top-left-radius: 0.3rem;
  border-left: 1px solid #d3d9e3;
}

th:last-child {
  border-top-right-radius: 0.3rem;
}

td {
  border-top: 1px solid #d3d9e3;  
  border-right: 1px solid #d3d9e3;
  padding: 1rem;
}

td:first-child {
  border-left: 1px solid #d3d9e3;
}

tbody > tr:last-child td {
  border-bottom: 1px solid #d3d9e3;
}

.d2l-button.primary {
  background-color: #006fbf;
  color: #fff;
}

.d2l-button {
  margin: 10px;
  background-color: #f2f3f5;
  border-color: #d3d9e3;
  color: #565a5c;
  border-width: 1px;
  border-style: solid;
  border-radius: 0.3rem;
  box-sizing: border-box;
  cursor: pointer;
  display: inline-block;
  font-family: inherit;
  outline: none;
  padding: 0.5rem 1.5rem;
  box-shadow: 0 0 0 4px rgba(0, 0, 0, 0);
}

.d2l-button.primary:hover {
  background-color: #006fbf;
  color: #fff;
}

.d2l-button:hover {
  background-color: #e6eaf0;
}

.d2l-button:focus {
  border-color: rgba(0, 111, 191, 0.4);
  box-shadow: 0 0 0 4px rgba(0, 111, 191, 0.3);
}

.d2l-checkbox {
    -webkit-appearance: none;
    -moz-appearance: none;
    appearance: none;
    background-position: center center;
    background-repeat: no-repeat;
    background-size: 1.2rem 1.2rem;
    border-radius: 0.3rem;
    border-style: solid;
    box-sizing: border-box;
    display: inline-block;
    height: 1.2rem;
    margin: 0;
    padding: 0;
    transition-duration: 0.5s;
    transition-timing-function: ease;
    transition-property: background-color, border-color;
    vertical-align: middle;
    width: 1.2rem;
  }

  .d2l-checkbox:checked {
    background-image: url("data:image/svg+xml,%3Csvg%20xmlns%3D%22http%3A//www.w3.org/2000/svg%22%20width%3D%2224%22%20height%3D%2224%22%20viewBox%3D%220%200%2024%2024%22%3E%3Cpath%20fill%3D%22%23565A5C%22%20d%3D%22M8.4%2016.6c.6.6%201.5.6%202.1%200l8-8c.6-.6.6-1.5%200-2.1-.6-.6-1.5-.6-2.1%200l-6.9%207-1.9-1.9c-.6-.6-1.5-.6-2.1%200-.6.6-.6%201.5%200%202.1l2.9%202.9z%22/%3E%3C/svg%3E%0A");
  }
  
  .d2l-checkbox,
  .d2l-checkbox:hover:disabled {
    background-color: #f9fafb;
    border-width: 1px;
  }
  
  .d2l-checkbox:hover,
  .d2l-checkbox:focus {
    border-color: #006fbf;
    border-width: 2px;
    outline-width: 0;
  }

  .d2l-checkbox[aria-invalid="true"] {
    border-color: #cd2026;
  }

  .d2l-checkbox:disabled {
    opacity: 0.5;
  }

  /* Firefox only, fixed in Firefox 54 */
  /* https://bugzilla.mozilla.org/show_bug.cgi?id=605985 */
  @-moz-document url-prefix() {
    input[type="checkbox"] {
      -moz-appearance: checkbox;
    }
  }
</style>
