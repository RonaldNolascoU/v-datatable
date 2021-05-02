<template>
  <div class="flex flex-col">
    <div class="-my-2 overflow-x-auto sm:-mx-6 lg:-mx-8">
      <div class="py-2 align-middle inline-block min-w-full sm:px-6 lg:px-8">
        <div
          class="shadow overflow-hidden border-b border-gray-200 sm:rounded-lg"
        >
          <table class="min-w-full divide-y divide-gray-200">
            <thead class="bg-gray-50">
              <tr>
                <th
                  scope="col"
                  class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider"
                >
                  Type
                </th>
              </tr>
            </thead>
            <tbody class="bg-white divide-y divide-gray-200">
              <template v-for="row in users" :key="row.id">
                <tr @click="toggle(row)" class="bg-red-300 cursor-pointer">
                  <td class="py-4 whitespace-nowrap w-1/6">
                    <div class="flex items-center">
                      <div class="ml-4">
                        <div
                          class="text-sm font-medium text-gray-900"
                          @click="editField(row, 'name')"
                        >
                          <Input
                            v-if="row.editing && editingCell == 'name'"
                            :field="'name'"
                            :width="'w-2/3'"
                            :value="row.name"
                            @update:value="updateInfo(row, 'name', $event)"
                          />
                          <template v-else>{{ row.name }}</template>
                        </div>
                        <div class="text-sm text-gray-500"></div>
                      </div>
                    </div>
                  </td>
                  <td class="py-4 whitespace-nowrap w-1/6">
                    <div
                      class="text-sm font-medium text-gray-900"
                      @click="editField(row, 'count')"
                    >
                      <Input
                        v-if="row.editing && editingCell == 'count'"
                        :field="'count'"
                        :width="'w-2/3'"
                        :value="row.count"
                        @update:value="updateInfo(row, 'count', $event)"
                      />
                      <template v-else>{{ row.count }}</template>
                    </div>
                  </td>
                  <td class="px-6 py-4 whitespace-nowrap w-1/6"></td>
                </tr>
                <template v-if="opened.includes(row.id)">
                  <tr
                    v-for="info in row.info"
                    :key="info.id"
                    class="bg-yellow-300"
                  >
                    <td class="py-4 whitespace-nowrap"></td>
                    <td
                      class="py-4 whitespace-nowrap w-1/6"
                      @click="editField(info, 'name')"
                    >
                      <Input
                        v-if="info.editing && editingCell == 'name'"
                        :field="'name'"
                        :value="info.name"
                        @update:value="updateInfo(info, 'name', $event)"
                      />
                      <template v-else>{{ info.name }}</template>
                    </td>
                    <td
                      class="py-4 whitespace-nowrap w-1/6"
                      @click="editField(info, 'role')"
                    >
                      <Input
                        v-if="info.editing && editingCell == 'role'"
                        :field="'role'"
                        :value="info.role"
                        @update:value="updateInfo(info, 'role', $event)"
                      />
                      <template v-else>{{ info.role }}</template>
                    </td>
                  </tr>
                </template>
              </template>
            </tbody>
          </table>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Input from "./Input";
export default {
  data() {
    return {
      opened: [],
      editingCell: null,
      users: [
        {
          id: 1,
          name: "Superusers",
          count: "Count:2",
          info: [
            {
              name: "John Doe",
              role: "Accountant",
            },
            {
              name: "Jane Doe",
              role: "Merchant",
            },
          ],
        },
        {
          id: 2,
          name: "Users",
          count: "Count:1",
          info: [
            {
              name: "John Test",
              role: "Developer",
            },
          ],
        },
      ],
    };
  },
  components: { Input },
  methods: {
    // Toggle row expanding
    toggle(row) {
      // Prevent row expanding when editing
      if (row.editing) { return }
      const index = this.opened.indexOf(row.id);
      if (index > -1) {
        this.opened.splice(index, 1);
      } else {
        this.opened.push(row.id);
      }
    },
    editField(info, field) {
      // Setting editing field
      this.editingCell = field;
      info.editing = true;
    },
    updateInfo(info, field, value) {
      // Updating info property and stop edit
      info[field] = value;
      info.editing = false;
    },
  },
};
</script>

<style>
</style>