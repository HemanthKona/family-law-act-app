<template>
    <div v-if="dataReady">

        <!-- ******** IMPORTANT NOTE: ********
         Originally this was "Schedule 5 - Contact with a child". The new changes are now referring as "Schedule 3 - Contact with a child";
         however, this is included in "Schedule5.vue" file. The form and structure needs to be reviewed and clarified.
         ********************************* -->
        <div class="new-page" />
        <div style="display: flex; flex-direction: row; margin-bottom: 0.5rem;">
            <div style="width: 80%; padding-right: 4px;">
                <ScheduleHeader scheduleNumber="Schedule 3" scheduleTitle="Contact with a child" scheduleDescription="Disagree with order requested by other party"></ScheduleHeader>
                <div style="margin-bottom: 0.5rem;"></div>
                <NoteBox>
                        Complete this schedule only if you disagree with all or part of the order about contact with a child applied for by the other party on Schedule 5 or Schedule 6 of their Application About a Family Law Matter.
                </NoteBox>
            </div>
            <div style="width: 20%;"></div>
        </div>

        <!-- <Part 1> -->
        <div style="display: flex; flex-direction: row;">
            <div style="width: 80%; padding-right: 4px;">
                <FormPart :part="1" title="Reason you disagree" style="margin-bottom: 0rem;"></FormPart>
                <div style="margin-left: 1rem; text-indent: -10px; padding-left: 10px;">
                    <b>1. I do not agree with the order requested</b> by the other party about contact with a child, because:
                </div>
                <div v-if="chContInfo.abt.otherComm" style="margin-left: 1rem; margin-top: 0; background-color: #dedede;padding:10px;font-size: 11pt;margin-left:30px;min-height:190px;">
                    {{chContInfo.abt.otherComm}}
                </div>
                <div style="margin-left: 1.5rem; margin-top: 0; margin-bottom: 1rem;">
                    <GreyBoxForm v-if="!chContInfo.abt.otherComm" style="margin-top:5px; text-indent:0rem;" textwidth="32rem" :text="chContInfo.abt.otherComm"></GreyBoxForm>
                </div>
            </div>
            <div style="width: 20%;"></div>
        </div>

        <!-- <Part 2> -->
        <div style="display: flex; flex-direction: row;">
            <div style="width: 80%; padding-right: 4px;">
                <FormPart :part="2" title="Existing final order or agreement" subtitle="Complete this part only if there is an existing order or agreement about contact with a child"></FormPart>
                <div style="margin-left: 1rem;">
                    <b>2. </b><i>Select only one of the options below</i>
                    <check-box :shift="10" :shiftmark="1" :boxMargin="0" :check="false?'yes':''" text="I would like the final order or agreement to <b>continue to be in place</b> ➜ <i>If you selected this option, no further information is required on this schedule<i>"/>
                    <check-box :shift="10" :shiftmark="1" :boxMargin="0" :check="false?'yes':''" text="I am applying for the final order or agreement to be <b>changed, suspended or replaced</b> as set out in Part 3"/>
                </div>
            </div>
            <div style="width: 20%;"></div>
        </div>

        <!-- <Part 3> -->
        <div style="display: flex; flex-direction: row;">
            <div style="width: 80%; padding-right: 4px;">
                <FormPart :part="3" title="Order about contact with a child" subtitle="You do not need to complete this part if have indicated you would like the existing order or agreement to continue to be in place."></FormPart>
                <div style="margin-left: 1rem; text-indent: -10px; padding-left: 10px;">
                    <b>3. </b> I am applying for an order for the child(ren) to have <b>contact with a person <u>who is not their guardian</u></b> as follows:<br />
                    <i>Select all options that apply and complete the required information</i>
                </div>

                <div style="margin:0 0 1rem 1rem;">
                    <check-box :shift="10" :shiftmark="1" :boxMargin="0" :check="chContInfo.abt.conType.inPerson?'yes':''" text="In person <i>(specify)</i>:"/>
                    <div style="margin-left: 1.5rem; text-indent: -5px; padding-left: 5px;">
                        <i>Provide details including specific dates or events requested, or dates and times that would be most suitable</i>
                    </div>
                    <div v-if="chContInfo.abt.inPrsn" style="margin-left: 1.5rem; margin-top: 0; background-color: #dedede;padding:10px;font-size: 11pt;margin-left:30px;min-height:190px;">
                        {{chContInfo.abt.inPrsn}}
                    </div>
                    <GreyBoxForm v-if="!chContInfo.abt.inPrsn" style="margin-top:5px; margin-left:1.5rem; text-indent:0rem" textwidth="31rem" :text="chContInfo.abt.inPrsn"></GreyBoxForm>
                    <check-box :shift="10" :shiftmark="1" :boxMargin="0" :check="chContInfo.abt.conType.tel?'yes':''" text="Telephone communication"/>
                    <check-box :shift="10" :shiftmark="1" :boxMargin="0" :check="chContInfo.abt.conType.video?'yes':''" text="Video communication"/>
                    <check-box :shift="10" :shiftmark="1" :boxMargin="0" :check="chContInfo.abt.conType.written?'yes':''" text="Written communication"/>
                    <check-box :shift="10" :shiftmark="1" :boxMargin="0" :check="chContInfo.abt.conType.other?'yes':''" text="Other method of communication <i>(specify):</i>"/>
                    
                    <div v-if="chContInfo.abt.otherComm" style="margin-left: 1rem; margin-top: 0; background-color: #dedede;padding:10px;font-size: 11pt;margin-left:30px;min-height:100px;">
                        {{chContInfo.abt.otherComm}}
                    </div>
                    <GreyBoxForm v-if="!chContInfo.abt.otherComm" style="margin-top:5px; margin-left:1.5rem; text-indent:0rem" textwidth="31rem" :text="chContInfo.abt.otherComm"></GreyBoxForm>
                </div>

                <div style="margin-left: 1rem;">
                    <b>4. </b> <i>Complete if applicable. You may leave this question blank</i>.
                    <div style="margin-left: 1rem;">I am applying for <b>additional terms about contact</b> with a child as follows:</div>
                    <div style="margin-left: 1rem;"><i>List the details of the terms you are asking for</i></div>
                    <div v-if="chContInfo.abt.otherComm" style="margin-left: 1rem; margin-top: 0; background-color: #dedede;padding:10px;font-size: 11pt;margin-left:30px;min-height:100px;">
                        {{chContInfo.abt.otherComm}}
                    </div>
                    <GreyBoxForm v-if="!chContInfo.abt.otherComm" style="margin-top:5px; margin-left:1rem; text-indent:0rem" textwidth="31.5rem" :text="chContInfo.abt.otherComm"></GreyBoxForm>
                    
                </div>

            </div>
            <div style="width: 20%;">
                <NoteBox>
                    <b-icon-info-circle-fill />
                    <p>
                        The court may make an order about contact with a child, including describing the terms and form of contact [s. 59 <i>Family Law Act</i>]. 
                    </p>
                </NoteBox>
            </div>
        </div>

        <!-- <Part 4> -->
        <div style="display: flex; flex-direction: row;">
            <div style="width: 80%; padding-right: 4px;">
                <FormPart :part="4" title="Best interests of the child" subtitle="You do not need to complete this part if have indicated you would like the existing order or agreement to continue to be in place."></FormPart>
                <div style="margin-left: 1rem; text-indent: -10px; padding-left: 10px;">
                    <b>5. </b> I believe the order about contact with a child that I am applying for is in the <b>best interests of the child(ren)</b> because:<br />
                    <i>List your reasons</i>
                </div>

                <div v-if="chContInfo.abt.otherComm" style="margin-left: 1rem; margin-top: 0; background-color: #dedede;padding:10px;font-size: 11pt;margin-left:30px;min-height:400px;">
                    {{chContInfo.abt.otherComm}}
                </div>
                <div style="margin-left: 1.5rem; margin-top: 0; margin-bottom: 1rem;">
                    <GreyBoxForm v-if="!chContInfo.abt.otherComm" style="margin-top:5px; text-indent:0rem;" textwidth="32rem" :text="chContInfo.abt.otherComm"></GreyBoxForm>
                </div>
            </div>
            <div style="width: 20%;">
                <NoteBox>
                    <b-icon-info-circle-fill />
                    <p>
                        To determine what is in the best interests of a child, all of the child’s needs and circumstances must be considered including the factors set out in s. 37 of the <i>Family Law Act.</i><br />
                        The parties and the court must consider the best interests of a child when making a decision about contact with a child. For more information, see the guidebook. 
                    </p>
                </NoteBox>
            </div>
        </div>

        <div style="margin-top: 1rem;"></div>
    </div>
</template>

<script lang="ts">
import { Component, Prop, Vue } from 'vue-property-decorator';
import UnderlineForm from "@/components/utils/PopulateForms/components/UnderlineForm.vue";
import CheckBox from "@/components/utils/PopulateForms/components/CheckBox.vue";
import { schedule5DataInfoType } from '@/types/Application/ReplyFamilyLawMatter/Pdf';
import NoteBox from '@/components/utils/PopulateForms/components/NoteBox.vue';
import FormPart from '@/components/utils/PopulateForms/components/FormPart.vue';
import ScheduleHeader from '@/components/utils/PopulateForms/components/ScheduleHeader.vue';
import GreyBoxForm from '@/components/utils/PopulateForms/components/GreyBoxForm.vue';

@Component({
    components:{
        UnderlineForm,
        CheckBox,
        NoteBox,
        FormPart,
        ScheduleHeader,
        GreyBoxForm
    }
})
export default class Schedule5 extends Vue {

    @Prop({required:true})
    result!: any;
    
    dataReady = false;
    chContInfo = {} as schedule5DataInfoType;   
   
    mounted(){
        this.dataReady = false;   
        this.extractInfo();       
        this.dataReady = true;        
    }

    public extractInfo(){ 
        console.log(this.result)
        this.chContInfo = this.getNewChildContactInfo();
    }   

    public getNewChildContactInfo(){

        let newChildContactInfo = {} as schedule5DataInfoType;  
        
        newChildContactInfo.abt = {
            conType: {
                noContact: false,
                inPerson: false,
                tel: false,
                video: false,
                written:false,
                other: false
            },
            inPrsn: '',
            otherComm: '',
            cond: ''            
        };
        newChildContactInfo.bstIntrst = '';

        if (this.result.disagreeContactWithChildSurvey){
            const disagreeInfo = this.result.disagreeContactWithChildSurvey;
            const contactChoices = disagreeInfo.contactTypeChoices?disagreeInfo.contactTypeChoices:[];
            newChildContactInfo.abt = {
                conType: {
                    noContact: contactChoices.includes('No contact of any type'),
                    inPerson: contactChoices.includes('In person'),
                    tel: contactChoices.includes('Telephone communication'),
                    video: contactChoices.includes('Video communication'),
                    written:contactChoices.includes('Written communication'),
                    other: contactChoices.includes('other')
                },
                inPrsn: (contactChoices.includes('In person'))? disagreeInfo.inPersonDetails:'',
                otherComm: (contactChoices.includes('other'))? disagreeInfo.contactTypeChoicesComment:'',
                cond: (disagreeInfo.placeConditions == 'y')? disagreeInfo.conditionsDescription:''                
            }
            newChildContactInfo.bstIntrst = disagreeInfo.childBestInterestReason?disagreeInfo.childBestInterestReason:'';
        }        

        return newChildContactInfo;
    }  

}
</script>

<style scoped lang="scss" src="@/styles/_pdf.scss">

</style> 