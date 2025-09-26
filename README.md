# Infinite-cascading
无限级联菜单；全国行政区划（省，市，县/区，乡/镇，村委会）；商品和服务税收分类编码表；

```
// 源数据(默认二维数组，适用简单信息；json格式适用于更多信息，编码作为键值用于无限级联获取子项列表）

var data=[['1','货物'],['101','农、林、牧、渔业类产品'],['10101','农业产品']];
// 定义各级编码长度；0获取默认获取一级分类；
var reg=[0,1,3,5,7,9,11,13,15,17,19];


function get_subcase(arr, reg, code = null) { //长码+短码通用
	let res = [],
		c_p, //父级
		c_c, //当前级别
		c_n; //下属级别
		let l =!code?0:reg.indexOf(code.length);
	arr.forEach((n) => {
		c_p =!code?null:n[0].slice(0, reg[l]);
		c_c = n[0].slice(reg[l], reg[l + 1]);
		c_n = n[0].slice(reg[l + 1]);
		if (c_p == code && c_c != 0 && c_n == 0) {
			res.push([c_p == null ? c_c : c_p + c_c, n[1]]);
		}
	});
	return res;
}
```
