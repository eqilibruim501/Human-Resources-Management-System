<template>
  <div>
    <hr>

    <router-link :to="{ name:'attendance.attendance-form' }">
      <button type="button" class="btn btn-success btn-sm float-right" data-tooltip="true" title="Attendance Form">
        <i class="fas fa-plus" />
      </button>
    </router-link>

    <h4 class="card-title">
      {{ $t('attendance_list.attendance_list') }}
    </h4>

    <hr>

    <data-grid ref="dataGrid" url="/api/users/attendance" element-id="attendance" :headers="headers">
      <template #item.actions="{ item }">
        <div class="dropdown dropleft">
          <a href="#" role="button" data-toggle="dropdown" aria-expanded="true" class="btn btn-secondary btn-sm dropdown-toggle">
            <i class="fas fa-ellipsis-v fa-fw" />
          </a>

          <div class="dropdown-menu dropdown-menu-right">
            <router-link :to="{name:'attendance.attendance-edit', params: {id: item.id} }" class="dropdown-item">
              <i class="fas fa-pen fa-fw" /> {{ $t('general.edit') }}
            </router-link>

            <router-link :to="{name:'attendance.attendance-delete', params: {id: item.id} }" class="dropdown-item text-danger btn-delete">
              <i class="fas fa-trash fa-fw" /> {{ $t('general.delete') }}
            </router-link>
          </div>
        </div>
      </template>
    </data-grid>

    <router-view />
  </div>
</template>

<script>
    import DataGrid from '../../../datagrid/datagrid';

    export default {
        components: {
            DataGrid
        },

        data: (self = this) => ({
            headers: [
                {text: self.$i18n.t('form.employee'), value: 'employee_id', width: '200px', sortable: false},
                {text: self.$i18n.t('form.time_in'), value: 'time_in_date', width: '200px', sortable: false},
                {text: self.$i18n.t('form.time_out'), value: 'time_out_date', width: '200px', sortable: false},
                {text: '', value: 'actions', width: '40px', sortable: false},
            ]
        }),
    }
</script>
