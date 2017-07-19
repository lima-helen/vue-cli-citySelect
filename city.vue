<el-form :model="dialogForm" :rules="rules" ref="dialogForm" class="demo-ruleForm" >

    <el-form-item label="名称"  prop="name">
        <el-input v-model="dialogForm.name"  placeholder="名称" type="text"  auto-complete="off"></el-input>
    </el-form-item>

    <el-form-item label="选择地区：" required>
        <el-col :span="6">
            <el-form-item prop="selectProv">
                <el-select size="small" style="width: 100%" v-model="dialogForm.selectProv" v-on:change="getProv($event)" filterable placeholder="请选择省份">
                    <el-option :value="n" :key="index" :label="n" v-for="(n,index) in dataProv[0]['prov']">
                    </el-option>
                </el-select>
            </el-form-item>
        </el-col>

        <el-col :span="6">
            <el-form-item prop="selectCity">
                <el-select size="small" style="width: 100%" v-model="dialogForm.selectCity" v-on:change="getCity($event)" filterable  placeholder="请选择城市">
                    <el-option :value="n" :key="index" :label="n" v-for="(n,index) in dataCity">

                    </el-option>
                </el-select>
            </el-form-item>
        </el-col>
        <el-col :span="6">
            <el-form-item prop="selectCountry">
                <el-select size="small" style="width:100%" v-model="dialogForm.selectCountry" filterable  placeholder="请选择镇，县">
                    <el-option :value="n" :key="index" :label="n" v-for="(n,index) in dataCountry"></el-option>
                </el-select>
            </el-form-item>
        </el-col>

    </el-form-item>
</el-form>
<script>
    import cityJson from './data/city.json'
    export default {
        data() {
        return {
            cityDetail:"",
            dataProv:cityJson['selectProv'],
            dataCity:"",
            dataCountry:"",
            provIndex:"",
            cityIndex:"",
            dialogForm: {
                name: '',
                selectProv:"",
                selectCity: '',
                selectCountry:"",
                mark:''
            },
            selectItems:[],
            rules: {
                name: [
                    { required: true, message: '请输入街道名称', trigger: 'blur' }
                ],
                selectProv: [
                    { required: true, message: '请选择省份', trigger: 'change' }
                ],
                selectCity: [
                    { required: true, message: '请选择城市', trigger: 'change' }
                ],
                selectCountry: [
                    { required: true, message: '请选择市区', trigger: 'change' }
                ]
            },
            dialogFormFenLeiVisible:false,
            tableData: dataTable['tableData'],
            multipleSelection: [],
            isActive:true

        }
    },
    methods: {
        getProv:function(prov){
            this.provIndex=this.dataProv[0]["prov"].indexOf(prov);
            this.dataCity=this.dataProv[this.provIndex+1]["0_"+this.provIndex];

            this.dialogForm.selectCity=this.dataCity[0];
            this.cityDetail=this.dataProv[this.provIndex+1]["class1"];
            this.dataCountry=this.cityDetail[0]["class2"];

            this.dialogForm.selectCountry=this.dataCountry[0];

        },
        getCity:function(city){
            this.cityIndex=this.dataCity.indexOf(city);
            this.dataCountry=this.cityDetail[this.cityIndex]["class2"];
            this.dialogForm.selectCountry=this.dataCountry[0];
        },
    }
    }
</script>