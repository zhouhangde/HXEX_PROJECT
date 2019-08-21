<template>
	<div class="LegalTrade_addBank">
		   <div style="width: 400px;margin: 0 auto;background: #131625;color: #fff;padding: 19px;">
				<div style="display: flex;justify-content: space-between;margin-left: 14px;padding: 10px 0;"> 
					<span>开户名:</span>
					<div style="margin-left: 11px;flex-grow: 1;">
						<input value="王玉晓" style="background: none;border: 1px solid #bbb2b2;padding: 3px;width: 100%;"/>
						<p style="color: red;font-size: 14px;padding: 3px 0;">提示:只添加本人名下的银行卡</p>
					</div>
				</div>
				<div style="display: flex;justify-content: space-between;margin-left: 14px;padding: 10px 0;"> 
					<span>开户银行:</span>
					<div style="margin-left: 11px;flex-grow: 1;">
						<select style="padding: 5px 0;margin: 0px;width: 100%;font-size: 9px;">                                        
							<option style="text-align:center;">请选择银行</option>                                    
						</select>
						<p style="color: red;font-size: 14px;padding: 3px 0;">人民币提现仅支持列表中的银行</p>
					</div>
				</div>
				<div style="display: flex;justify-content: space-between;margin-left: 14px;padding: 12px 0;"> 
					<span>开户银行所在地:</span>
					<select style="padding: 5px 0;margin: 0px;font-size: 9px;flex-grow: 1;margin-left: 16px;">                                        
						<option style="text-align:center;">选择省</option>                                    
					</select>
					<select style="padding: 5px 0;margin: 0px;font-size: 9px;flex-grow: 1;margin-left: 16px;">                                        
						<option style="text-align:center;">选择市</option>                                    
					</select>
				</div>
				<div style="display: flex;justify-content: space-between;margin-left: 14px;padding: 12px 0;"> 
					<span>开户支行名称:</span>
					<div style="margin-left: 11px;flex-grow: 1;">
						<input value="王玉晓" style="background: none;color: #fff;border: 1px solid #bbb2b2;padding: 3px;width: 100%;"/>
					</div>
				</div>
				<div style="display: flex;justify-content: space-between;margin-left: 14px;padding: 12px 0;"> 
					<span>银行卡号:</span>
					<div style="margin-left: 11px;flex-grow: 1;">
						<input value="请填写正确的银行卡号，不用空格隔开" style="background: none;color: #fff;border: 1px solid #bbb2b2;padding: 3px;width: 100%;"/>
					</div>
				</div>
				<div style="display: flex;justify-content: space-between;margin-left: 14px;padding: 12px 0;"> 
					<span>重复卡号:</span>
					<div style="margin-left: 11px;flex-grow: 1;">
						<input value="" style="background: none;border: 1px solid #bbb2b2;color: #fff;padding: 3px;width: 100%;"/>
					</div>
				</div>
			</div>
        <!-- 整个内容结束 -->
	</div>
</template>

<script>
	export default {
		name: "LegalTrade_addBank",
		data() {
			return {
				
			};
		},
        props: {
		}, 
		created() {
			
		},
		filters: {
			
		},
		methods: {

		}
	};
</script>

<style scoped>
  
</style>>
