// global variable
let config  = (function() {
	
	var batchType = 'device',
		param = {};
	
	return {
		getBatchType: function() {
			return batchType;
		},
		
		getParam: function() {
			return param;
		}
	}
})();

// how to use
config.getBatchType()
