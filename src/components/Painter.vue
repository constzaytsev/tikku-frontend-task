<template>
  <div class="painter is-row is-col-stack-24 is-inset-top-24 is-border-bottom">
    <div class="is-col is-20 painter__image-container">
      <img :src="`data:image/png;base64,${painter.Logo}`" alt="" />
    </div>
    <div class="is-col is-60">
      <h4 class="is-stack-12">{{ painter.Name }}</h4>
      <div class="is-stack-8 is-small">
        <div class="icon-pointer"></div>
        {{ painter.City }}
      </div>
      <div class="is-container is-stack-12 is-small">
        <div class="is-inset-right-24">
          <div class="icon-phone"></div>
          {{ painter.PhoneNumber }}
        </div>
        <div>
          <div class="icon-mail"></div>
          <a v-if="painter.Email" :href="`mailto:${painter.Email}`">{{
            painter.Email
          }}</a>
        </div>
      </div>
      <div class="is-small is-muted" v-html="painter.Description"></div>
    </div>
    <div class="is-col is-text-center is-20">
      <div class="is-stack-24">
        <button class="button is-secondary">Pyydä tarjous!</button>
      </div>
      {{ painter.NumberOfProjects }}
      <div class="is-smaller">Projects</div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    painter: {
      type: Object,
      default: () => {
        return {};
      }
    }
  }
};
</script>

<style lang="scss">
.painter {
  transition: background 0.3s;

  &:hover {
    background-color: #eee;
  }

  a {
    border-bottom: 2px solid rgb(239, 65, 53);
  }
}

.icon-pointer,
.icon-phone,
.icon-mail {
  display: inline-block;
  vertical-align: middle;
  margin-right: 4px;
  width: 24px;
  height: 24px;
  opacity: 0.5;
  background: {
    size: 20px;
    repeat: no-repeat;
    position: center center;
  }
}

.icon-pointer {
   background-image: url(data:image/svg+xml;base64,PD94bWwgdmVyc2lvbj0iMS4wIiA/Pjxzdmcgdmlld0JveD0iMCAwIDMyIDMyIiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciPjx0aXRsZS8+PGcgaWQ9Ikljb25zIj48cGF0aCBkPSJNMTYsMkExMCwxMCwwLDAsMCw2LDEyYzAsOCw4LjksMTcuMyw5LjI4LDE3LjY5YTEsMSwwLDAsMCwxLjQ0LDBDMTcuMSwyOS4zLDI2LDIwLDI2LDEyQTEwLDEwLDAsMCwwLDE2LDJabTAsMjUuNTFDMTMuOTEsMjUuMTQsOCwxNy45MSw4LDEyYTgsOCwwLDAsMSwxNiwwQzI0LDE3LjkxLDE4LjA5LDI1LjE0LDE2LDI3LjUxWiIvPjxwYXRoIGQ9Ik0xNiw3YTUsNSwwLDEsMCw1LDVBNSw1LDAsMCwwLDE2LDdabTAsOGEzLDMsMCwxLDEsMy0zQTMsMywwLDAsMSwxNiwxNVoiLz48L2c+PC9zdmc+);
}

.icon-phone {
  background-image: url(data:image/svg+xml;base64,PD94bWwgdmVyc2lvbj0iMS4wIiA/PjwhRE9DVFlQRSBzdmcgIFBVQkxJQyAnLS8vVzNDLy9EVEQgU1ZHIDEuMS8vRU4nICAnaHR0cDovL3d3dy53My5vcmcvR3JhcGhpY3MvU1ZHLzEuMS9EVEQvc3ZnMTEuZHRkJz48c3ZnIGVuYWJsZS1iYWNrZ3JvdW5kPSJuZXcgMCAwIDUwIDUwIiBoZWlnaHQ9IjUwcHgiIGlkPSJMYXllcl8xIiB2ZXJzaW9uPSIxLjEiIHZpZXdCb3g9IjAgMCA1MCA1MCIgd2lkdGg9IjUwcHgiIHhtbDpzcGFjZT0icHJlc2VydmUiIHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8yMDAwL3N2ZyIgeG1sbnM6eGxpbms9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGxpbmsiPjxyZWN0IGZpbGw9Im5vbmUiIGhlaWdodD0iNTAiIHdpZHRoPSI1MCIvPjxwYXRoIGQ9Ik0zMC4yMTcsMzUuMjUyYzAsMCw0LjA0OS0yLjMxOCw1LjEwOS0yLjg3NSAgYzEuMDU3LTAuNTU5LDIuMTUyLTAuNywyLjgxNy0wLjI5NGMxLjAwNywwLjYxNiw5LjQ2Myw2LjI0MSwxMC4xNzUsNi43MzljMC43MTIsMC40OTksMS4wNTUsMS45MjQsMC4wNzYsMy4zMiAgYy0wLjk3NSwxLjM5Ni01LjQ3Myw2LjkxNi03LjM3OSw2Ljg1N2MtMS45MDktMC4wNjItOS44NDYtMC4yMzYtMjQuODEzLTE1LjIwN0MxLjIzOCwxOC44MjYsMS4wNjEsMTAuODg3LDEsOC45NzggIEMwLjkzOSw3LjA3LDYuNDU5LDIuNTcxLDcuODU1LDEuNTk1YzEuMzk4LTAuOTc1LDIuODI1LTAuNjA4LDMuMzIxLDAuMDc4YzAuNTY0LDAuNzgxLDYuMTI0LDkuMjEsNi43MzYsMTAuMTc2ICBjMC40MTksMC42NiwwLjI2NSwxLjc2MS0wLjI5NCwyLjgxOWMtMC41NTYsMS4wNi0yLjg3NCw1LjEwOS0yLjg3NCw1LjEwOXMxLjYzNCwyLjc4Nyw3LjE2LDguMzEyICBDMjcuNDMxLDMzLjYxNSwzMC4yMTcsMzUuMjUyLDMwLjIxNywzNS4yNTJ6IiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgc3Ryb2tlLXdpZHRoPSIyIi8+PC9zdmc+);
}

.icon-mail {
  background-image: url(data:image/svg+xml;base64,PD94bWwgdmVyc2lvbj0iMS4wIiA/PjxzdmcgaGVpZ2h0PSIzMzEuNDY4OTkiIGlkPSJzdmcyNDM5IiB2ZXJzaW9uPSIxLjAiIHdpZHRoPSI0MzkuMzcxIiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHhtbG5zOmNjPSJodHRwOi8vY3JlYXRpdmVjb21tb25zLm9yZy9ucyMiIHhtbG5zOmRjPSJodHRwOi8vcHVybC5vcmcvZGMvZWxlbWVudHMvMS4xLyIgeG1sbnM6aW5rc2NhcGU9Imh0dHA6Ly93d3cuaW5rc2NhcGUub3JnL25hbWVzcGFjZXMvaW5rc2NhcGUiIHhtbG5zOnJkZj0iaHR0cDovL3d3dy53My5vcmcvMTk5OS8wMi8yMi1yZGYtc3ludGF4LW5zIyIgeG1sbnM6c29kaXBvZGk9Imh0dHA6Ly9zb2RpcG9kaS5zb3VyY2Vmb3JnZS5uZXQvRFREL3NvZGlwb2RpLTAuZHRkIiB4bWxuczpzdmc9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj48ZGVmcyBpZD0iZGVmczI0NDEiPjxtYXJrZXIgaWQ9IkFycm93RW5kIiBtYXJrZXJIZWlnaHQ9IjMiIG1hcmtlclVuaXRzPSJzdHJva2VXaWR0aCIgbWFya2VyV2lkdGg9IjQiIG9yaWVudD0iYXV0byIgcmVmWD0iMCIgcmVmWT0iNSIgdmlld0JveD0iMCAwIDEwIDEwIj48cGF0aCBkPSJNIDAsMCBMIDEwLDUgTCAwLDEwIEwgMCwwIHoiIGlkPSJwYXRoMjQ0NCIvPjwvbWFya2VyPjxtYXJrZXIgaWQ9IkFycm93U3RhcnQiIG1hcmtlckhlaWdodD0iMyIgbWFya2VyVW5pdHM9InN0cm9rZVdpZHRoIiBtYXJrZXJXaWR0aD0iNCIgb3JpZW50PSJhdXRvIiByZWZYPSIxMCIgcmVmWT0iNSIgdmlld0JveD0iMCAwIDEwIDEwIj48cGF0aCBkPSJNIDEwLDAgTCAwLDUgTCAxMCwxMCBMIDEwLDAgeiIgaWQ9InBhdGgyNDQ3Ii8+PC9tYXJrZXI+PC9kZWZzPjxnIGlkPSJnMjQ0OSIgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTE0NS4zMzA1LC0xNDUuMzMwNSkiPjxwYXRoIGQ9Ik0gNTY5LjM3NCw0NjEuNDcyIEwgNTY5LjM3NCwxNjAuNjU4IEwgMTYwLjY1OCwxNjAuNjU4IEwgMTYwLjY1OCw0NjEuNDcyIEwgNTY5LjM3NCw0NjEuNDcyIHoiIGlkPSJwYXRoMjQ1MSIgc3R5bGU9ImZpbGw6bm9uZTtzdHJva2U6IzAwMDAwMDtzdHJva2Utd2lkdGg6MzAuNjU1MDAwNjkiLz48cGF0aCBpZD0icGF0aDI0NTMiIHN0eWxlPSJmaWxsOm5vbmU7c3Ryb2tlOiMwMDAwMDA7c3Ryb2tlLXdpZHRoOjMwLjY1NTAwMDY5Ii8+PHBhdGggZD0iTSAxNjQuNDYsMTY0LjQ5IEwgMzQwLjc4LDM0My4xNTggQyAzNTMuODQ5LDM1Ni4zMjggMzc3LjYzLDM1Ni4xNzIgMzkwLjQyMywzNDMuMjc4IEwgNTY2LjYyMiwxNjUuOTI4IiBpZD0icGF0aDI0NTUiIHN0eWxlPSJmaWxsOm5vbmU7c3Ryb2tlOiMwMDAwMDA7c3Ryb2tlLXdpZHRoOjMwLjY1NTAwMDY5Ii8+PHBhdGggZD0iTSAxNzAuNTE1LDQ1MS41NjYgTCAzMDUuNjEsMzEzLjQ2IiBpZD0icGF0aDI0NTciIHN0eWxlPSJmaWxsOm5vbmU7c3Ryb2tlOiMwMDAwMDA7c3Ryb2tlLXdpZHRoOjMwLjY1NTAwMDY5Ii8+PHBhdGggZD0iTSA1NTcuOTY4LDQ0OS45NzQgTCA0MjYuNTE1LDMxNS4zNzUiIGlkPSJwYXRoMjQ1OSIgc3R5bGU9ImZpbGw6bm9uZTtzdHJva2U6IzAwMDAwMDtzdHJva2Utd2lkdGg6MzAuNjU1MDAwNjkiLz48L2c+PC9zdmc+);
}

@media (max-width: 700px) {
    .painter {
        padding: 24px;
    }

    h4,
    .painter__image-container {
        text-align: center;
    }
}

</style>
