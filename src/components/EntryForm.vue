<template>
  <DialogForm ref="dialogForm">
    <template v-slot:header>
      <h4 class="modal-title" v-if="insertMode">{{ labels.title_new }}</h4>
      <h4 class="modal-title" v-if="updateMode">{{ labels.title_edit }}</h4>
    </template>
    <template v-slot:default>
        <div class="row row-height">
          <div class="col-md-3 col-height col-label">
            <label for="username">{{ labels.username_label }}</label>
          </div>
          <div class="col-height col-md-6">            
            <div class="input-group has-validation" :class="{'has-error': v$.username.$error}">
              <InputMask ref="username" v-model="localData.username" id="username" picture="(50)x" :disabled="disabledKeyField" /> 
              <label class="required">*</label>
            </div>
            <span v-if="v$.username.$error" class="has-error">{{ v$.username.$errors[0].$message }}</span>
          </div>
        </div>
        <div class="row row-height" v-if="insertMode">
          <div class="col-md-3 col-height col-label">
              <label for="userpassword" class="control-label">{{ labels.userpassword_label }}</label>
						</div>
						<div class="col-height col-md-5">
                <div class="input-group">
                  <input type="text" ref="userpassword" v-model="localData.userpassword" id="userpassword" class="form-control input-md" tabindex="-1" readonly />
                  <a href="javascript:void(0);" class="input-group-addon input-group-append input-group-text" @click="copyPassword" tabindex="-1"><i class="fa fa-copy" aria-hidden="true"></i></a>
                </div>
						</div>
        </div>
        <div class="row row-height">
          <div class="col-md-3 col-height col-label">
            <label for="usertname">{{ labels.usertname_label }}</label>
          </div>
          <div class="col-height col-md-7">
            <div class="input-group has-validation" :class="{'has-error': v$.usertname.$error}">
              <input type="text" ref="usertname" v-model="localData.usertname" id="usertname" class="form-control input-md" maxlength="50" /> 
              <label class="required">*</label>
            </div>
            <span v-if="v$.usertname.$error" class="has-error">{{ v$.usertname.$errors[0].$message }}</span>
          </div>
        </div>
        <div class="row row-height">
          <div class="col-md-3 col-height col-label">
            <label for="usertsurname">{{ labels.usertsurname_label }}</label>
          </div>
          <div class="col-height col-md-7">
            <div class="input-group has-validation" :class="{'has-error': v$.usertsurname.$error}">
              <input type="text" ref="usertsurname" v-model="localData.usertsurname" id="usertsurname" class="form-control input-md" maxlength="50" /> 
              <label class="required">*</label>
            </div>
            <span v-if="v$.usertsurname.$error" class="has-error">{{ v$.usertsurname.$errors[0].$message }}</span>
          </div>
        </div>
        <div class="row row-height">
          <div class="col-md-3 col-height col-label">
            <label for="userename">{{ labels.userename_label }}</label>
          </div>
          <div class="col-height col-md-7">
            <div class="input-group has-validation" :class="{'has-error': v$.userename.$error}">
              <input type="text" ref="userename" v-model="localData.userename" id="userename" class="form-control input-md" maxlength="50" /> 
              <label class="required">*</label>
            </div>
            <span v-if="v$.userename.$error" class="has-error">{{ v$.userename.$errors[0].$message }}</span>
          </div>
        </div>
        <div class="row row-height">
          <div class="col-md-3 col-height col-label">
            <label for="useresurname">{{ labels.useresurname_label }}</label>
          </div>
          <div class="col-height col-md-7">
            <div class="input-group has-validation" :class="{'has-error': v$.useresurname.$error}">
              <input type="text" ref="useresurname" v-model="localData.useresurname" id="useresurname" class="form-control input-md" maxlength="50" /> 
              <label class="required">*</label>
            </div>
            <span v-if="v$.useresurname.$error" class="has-error">{{ v$.useresurname.$errors[0].$message }}</span>
          </div>
        </div>
        <div class="row row-height">
          <div class="col-md-3 col-height col-label">
            <label for="email">{{ labels.email_label }}</label>
          </div>
          <div class="col-height col-md-7">
            <div class="input-group has-validation" :class="{'has-error': v$.email.$error}">
              <input type="text" ref="email" v-model="localData.email" id="email" class="form-control input-md" maxlength="100" /> 
              <label class="required">*</label>
            </div>
            <span v-if="v$.email.$error" class="has-error">{{ v$.email.$errors[0].$message }}</span>
          </div>
        </div>
        <div class="row row-height">
          <div class="col-md-3 col-height col-label">
            <label for="mobile">{{ labels.mobile_label }}</label>
          </div>
          <div class="col-height col-md-5">
            <input ref="mobile" type="text" v-model="localData.mobile" id="mobile" class="form-control input-md" maxlength="50" />
          </div>
        </div>
        <div class="row row-height">
          <div class="col-md-3 col-height col-label">
            <label for="lineid">{{ labels.lineid_label }}</label>
          </div>
          <div class="col-height col-md-5">
            <input ref="lineid" type="text" v-model="localData.lineid" id="lineid" class="form-control input-md" maxlength="50" />
          </div>
        </div>
        <div class="row row-height">
          <div class="col-md-3 col-height col-label">
            <label>{{ labels.gender_label }}</label>
          </div>
          <div class="col-height col-md-2">
            <div class="form-check">
            <input ref="male" type="radio" id="male" value="M" v-model="localData.gender" class="form-control input-md form-check-input"/>
            <label for="male" class="form-check-label gender-label" title="Male">&nbsp;<em class="fa fa-male" aria-hidden="true"></em></label>
            </div>
          </div>
          <div class="col-height col-md-2">
            <div class="form-check">
            <input ref="female" type="radio" id="female" value="F" v-model="localData.gender" class="form-control input-md form-check-input"/>
            <label for="female" class="form-check-label gender-label" title="Female">&nbsp;<em class="fa fa-female" aria-hidden="true"></em></label>
            </div>
          </div>
          <span v-if="v$.gender.$error" class="has-error">{{ v$.gender.$errors[0].$message }}</span>
        </div>
        <div class="row row-height">
          <div class="col-md-3 col-height col-label">
            <label for="userbranch">{{ labels.userbranch_label }}</label>
          </div>
          <div class="col-height col-md-5">
            <select ref="userbranch" v-model="localData.userbranch" class="form-control input-md" id="userbranch">
              <option v-for="item in dataCategory.tcompbranch" :key="item.id" :value="item.id">{{item.text}}</option>
            </select>            
          </div>
        </div>
        <div class="row row-height" v-if="updateMode">
          <div class="col-md-3 col-height col-label">
            <label for="inactive">{{ labels.inactive_label }}</label>
          </div>
          <div class="col-height col-md-5">
            <select ref="inactive" v-model="localData.inactive" class="form-control input-md" id="inactive">
              <option v-for="item in dataCategory.tkactive" :key="item.id" :value="item.id">{{item.text}}</option>
            </select>            
          </div>
        </div>
    </template>
    <template v-slot:footer>
      <button ref="savebutton" id="savebutton" class="btn btn-dark btn-sm" @click="saveClick" v-if="insertMode"><em class="fa fa-save fa-btn-icon"></em>{{ labels.save_button }}</button>
      <button ref="updatebutton" id="updatebutton" class="btn btn-dark btn-sm" @click="updateClick" v-if="updateMode"><em class="fa fa-save fa-btn-icon"></em>{{ labels.update_button }}</button>
      <button id="canceldialogbutton" class="btn btn-dark btn-sm" data-dismiss="modal"><em class="fa fa-close fa-btn-icon"></em>{{ labels.cancel_button }}</button>
    </template>
  </DialogForm>
</template>
<style>
.gender-label { font-size: 20px; }
</style>
<script>
import { ref, computed, watch } from 'vue';
import { useVuelidate } from '@vuelidate/core';
import { required, helpers, email } from '@vuelidate/validators';
import $ from "jquery";
import { createNewPassword, DEFAULT_CONTENT_TYPE, getApiUrl, disableControls }  from '@willsofts/will-app';
import { startWaiting, stopWaiting, submitFailure, detectErrorResponse }  from '@willsofts/will-app';
import { confirmUpdate, confirmSave, confirmDelete, successbox, serializeParameters } from '@willsofts/will-app';
import { InputMask } from '@willsofts/will-control';
import DialogForm from './DialogForm.vue';

const APP_URL = "/api/sfte005";
const defaultData = {
  site: "",
  userid: "",
  userbranch: "",
  username: "",
  userpassword: "",
  usertname: "",
  usertsurname: "",
  userename: "",
  useresurname: "",
  email: "",
  mobile: "",
  lineid: "",
  gender: "M",
  inactive: "0",
};

export default {
  components: {
    DialogForm, InputMask
  },
  props: {
    modes: Object,
    labels: Object,
    dataCategory: Object
  },
  emits: ["data-saved","data-updated","data-deleted"],
  setup(props) {
    const mode = ref({action: "new", ...props.modes});
    const localData = ref({ ...defaultData }); 
    const disabledKeyField = ref(false);
    const reqalert = ref(props.labels.empty_alert);
    const emailalert = ref(props.labels.email_alert);
    const requiredMessage = () => {
      return helpers.withMessage(reqalert, required);
    }
    const emailMessage = () => {
      return helpers.withMessage(emailalert, email);
    }
    const validateRules = computed(() => { 
      return {
        username: { required: requiredMessage() },
        usertname: { required: requiredMessage() },
        usertsurname: { required: requiredMessage() },
        userename: { required: requiredMessage() },
        useresurname: { required: requiredMessage() },
        email: { required: requiredMessage(), email: emailMessage() },
        gender: { required: requiredMessage() },
      } 
    });
    const v$ = useVuelidate(validateRules, localData, { $lazy: true, $autoDirty: true });
    return { mode, v$, localData, disabledKeyField, reqalert, emailalert };
  },
  created() {
    watch(this.$props, (newProps) => {      
      this.reqalert = newProps.labels.empty_alert;
      this.emailalert = newProps.labels.email_alert;
    });
  },
  computed: {
    insertMode() {
      return this.mode.action=="insert" || this.mode.action=="new";
    },
    updateMode() {
      return this.mode.action=="update" || this.mode.action=="edit";
    },
  },
  mounted() {
    this.$nextTick(function () {
      $("#modaldialog_layer").find(".modal-dialog").draggable();
    });
  },
  methods: {
    reset(newData,newMode) {
      if(newData) this.localData = {...newData};
      if(newMode) this.mode = {...newMode};
    },
    submit() {      
      this.$emit('update:formData', this.localData);
    },
    async saveClick() {
      console.log("click: save");
      disableControls($("#savebutton"));
      let valid = await this.validateForm();
      if(!valid) return;
      this.startSaveRecord();
    },
    async updateClick() {
      console.log("click: update");
      disableControls($("#updatebutton"));
      let valid = await this.validateForm();
      if(!valid) return;
      this.startUpdateRecord();
    },
    async validateForm(focusing=true) {
      const valid = await this.v$.$validate();
      console.log("validate form: valid",valid);
      console.log("error:",this.v$.$errors);
      if(!valid) {
        if(focusing) {
          this.focusFirstError();
        }
        return false;
      }
      return true;
    },
    focusFirstError() {
      if(this.v$.$errors && this.v$.$errors.length > 0) {
        let input = this.v$.$errors[0].$property;
        let el = this.$refs[input];
        if(el) el.focus(); //if using ref
        else $("#"+input).trigger("focus"); //if using id
      }
    },
    showDialog(callback) {
      //$("#modaldialog_layer").modal("show");
      if(callback) $(this.$refs.dialogForm.$el).on("shown.bs.modal",callback);
      $(this.$refs.dialogForm.$el).modal("show");
    },  
    hideDialog() {
      //$("#modaldialog_layer").modal("hide");
      $(this.$refs.dialogForm.$el).modal("hide");
    },
    resetRecord() {
      //reset to default data 
      this.reset(defaultData,{action:"insert"});
      this.localData.userpassword = createNewPassword();
      //reset validator
      this.v$.$reset();
      //enable key field
      this.disabledKeyField = false;
    },
    startInsertRecord() {
      this.resetRecord();
      this.showDialog(() => { this.$refs.username.focus(); });
    },
    startSaveRecord() {
      confirmSave(() => {
        this.saveRecord(this.localData);
      });
    },
    startUpdateRecord() {
      confirmUpdate(() => { 
        this.updateRecord(this.localData);
      });
    },
    startDeleteRecord(dataKeys) {
      confirmDelete(Object.values(dataKeys),() => {
        this.deleteRecord(dataKeys);
      });
    },
    saveRecord(dataRecord) {
        let jsondata = {ajax: true};
        let formdata = serializeParameters(jsondata,dataRecord);
        startWaiting();
        $.ajax({
          url: getApiUrl()+APP_URL+"/insert",
          data: formdata.jsondata,
          headers : formdata.headers,
          type: "POST",
          dataType: "json",
          contentType: DEFAULT_CONTENT_TYPE,
          error : function(transport,status,errorThrown) {
            console.error("error: status",status,"errorThrown",errorThrown);
            submitFailure(transport,status,errorThrown);
          },
          success: (data) => {
            stopWaiting();
            console.log("success",data);
            if(detectErrorResponse(data)) return;
            successbox(() => {
              //reset data for new record insert
              this.resetRecord();
              setTimeout(() => { this.$refs.username.focus(); },100);
              this.$emit('data-saved',dataRecord,data);
            });
          }
      });
    },
    updateRecord(dataRecord) {
        let jsondata = {ajax: true};
        let formdata = serializeParameters(jsondata,dataRecord);
        startWaiting();
        $.ajax({
          url: getApiUrl()+APP_URL+"/update",
          data: formdata.jsondata,
          headers : formdata.headers,
          type: "POST",
          dataType: "json",
          contentType: DEFAULT_CONTENT_TYPE,
          error : function(transport,status,errorThrown) {
            console.error("error: status",status,"errorThrown",errorThrown);
            submitFailure(transport,status,errorThrown);
          },
          success: (data) => {
            stopWaiting();
            console.log("success",data);
            if(detectErrorResponse(data)) return;
            successbox(() => {
              this.hideDialog();
              this.$emit('data-updated',dataRecord,data);
            });
          }
      });
    },
    retrieveRecord(dataKeys) {
      let jsondata = {ajax: true};
      let formdata = serializeParameters(jsondata,dataKeys);
      startWaiting();
      $.ajax({
        url: getApiUrl()+APP_URL+"/retrieve",
        data: formdata.jsondata,
        headers : formdata.headers,
        type: "POST",
        dataType: "json",
        contentType: DEFAULT_CONTENT_TYPE,
        error : function(transport,status,errorThrown) {
          console.error("retrieveRecord: error: status",status,"errorThrown",errorThrown);
          submitFailure(transport,status,errorThrown);
        },
        success: (data) => {
          stopWaiting();
          console.log("retrieveRecord: success",data);
          if(data.body.dataset) {
            this.reset(data.body.dataset,{action:"edit"});
            this.v$.$reset();
            this.disabledKeyField = true;
            this.showDialog(() => { this.$refs.usertname.focus(); });
          }
        }
      });	
    },
    deleteRecord(dataKeys) {
      let jsondata = {ajax: true};
      let formdata = serializeParameters(jsondata,dataKeys);
      startWaiting();
      $.ajax({
        url: getApiUrl()+APP_URL+"/remove",
        data: formdata.jsondata,
        headers : formdata.headers,
        type: "POST",
        dataType: "json",
        contentType: DEFAULT_CONTENT_TYPE,
        error : function(transport,status,errorThrown) {
          console.error("deleteRecord: error: status",status,"errorThrown",errorThrown);
          submitFailure(transport,status,errorThrown);
        },
        success: (data) => {
          stopWaiting();
          console.log("deleteRecord: success",data);
          if(detectErrorResponse(data)) return;
          successbox(() => {
            this.$emit('data-deleted',dataKeys,data);
          });
        }
      });	
    },
    async copyPassword() {
      try {
        let copyText = document.getElementById("userpassword");
        copyText.select();
        await navigator.clipboard.writeText(copyText.value);
      } catch(ex) { console.error(ex); }
    },
  }
};
</script>
