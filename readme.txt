相关说明：
    1、开发工具为:myeclipse11或以上,Spring,hibernate,springmvc,前端使用freemarker 
    2、数据库：mysql5.x，数据库文件于db文件目录下面
    3、服务器：tomcat7.x
    4、数据库配置于applicationContext.xml文件中
    5、后台登陆地址：http://xxxx:8080/login.do
                    用户名：admin 
                    密码：123456 
                    （默认商户与管理员都是)
    6、网站必须放置于服务器根目录下面，
       myeclipse配置方法http://jingyan.baidu.com/article/eae07827a945b61fed548544.html
    
目录说明：
    1、WebRoot/file:
            数据库设计概要：数据库设计概要（为上一个电商平台，做为参考)
            limmai.cdm: PowerDesign 设计（做为参考）
            wxpay: 微信支付小项目源码，可直接使用
    2、src/sms:
            短信第三方接口; 
    3、WebRoot/dist:
            css/js/js插件
    4、webRoot/WEB-INF/page:
            manager:后台管理员
            index:前台页面
            rsp:仿ajax返回



韦英飘：任务日记
	/manager/orders/listtakeoutProv.html
		110行   '提交时间','预定时间' 位置调换
		149-159行    位置调换
		
	/index/orders/ordertakeoutsec.html
		164-229行 
				
	/index/comments	
		添加toAdd.html
		添加toAppend.html
		
	src/sms/Sms.java 27行 变量 p2值为3 
	
	src/com/sunspot/service/CommentsService.java 添加 42行-93行
	
	src/com/sunspot/service/CommentsServiceImpl.java	添加 170-323行	

	/src/com/sunspot/service/OrdersServiceImpl.java 添加 第342行 ，434行
	
	/src/com/sunspot/controller/index/CommentsIndexController.java 是新添加的类
	
	2015-11-21
	Fresh.java ，FarmProduce.java 添加上架判断
	
	ALTER TABLE cookbook MODIFY IS_SHEL INTEGER(2) DEFAULT 0;
	
	ALTER TABLE fresh ADD IS_SHEL INTEGER(2) DEFAULT 0;
	
	ALTER TABLE farm_produce ADD IS_SHEL INTEGER(2) DEFAULT 0;
	
	
	
	黄祖源
	
	黄祖源 任务日志：
	1、com.sunspot.controller.manager.OrdersController类里面send方法里面添加
		ordersService.autoReceiveGoods(orderId, shop.getShopId());
	2、com.sunspot.service.impl.OrdersServiceImpl
			添加自动收货方法autoReceiveGoods(String, String);
			

	2015-12-4
	韦英飘 修改为‘+‘ 删除为’-‘
	com/sunspot/controller/index/MyIndexController
		217行 	+customer.setStatus(0); //注册时帐号正常
	WEB-INF/page/index/index/toRegister.html
		66行 		+<input type="checkbox" style="width:32px;height:32px;" name="accept" id="accept">
	WEB-INF/page/index/index/toRegShop.html
		68行		+<input type="checkbox" style="width:32px;height:32px;" name="accept" id="accept">
	com/sunspot/controller/index/DinnerIndexController
		224-245行
			/**
     		* 根据订单Id,查询商品信息
    		* @param orderId
    		* @param modelMap
     		* @param session
     		* @author scatlet
     		*/
    		public void details(String orderId,ModelMap modelMap,HttpSession session)
    		{
    			modelMap.addAttribute("weekDay", Utils.getWeekDay());
        		modelMap.addAttribute("curTime", Utils.getCurDate("HH:mm"));
        		List<CookbookExt> cookbook=cookbookService.queryCookBookByOrder(orderId);
        		List<CookbookIndexExt> list=new ArrayList<CookbookIndexExt>();
        
        		//收藏
        		for(CookbookExt c:cookbook){
        			CookbookIndexExt cookbookIndexExt=cookbookService.queryByIndexId(c.getCookbooksId());
        			list.add(cookbookIndexExt);
        			cheskShopLike(modelMap, session, c.getCookbooksId(), 1) ;
        		}
        		modelMap.addAttribute("list", list);
   			}
   		WEB-INF/page/index/index/myConsume.html
   			46行   	+<li class="clearFix" onclick="/index/dinner/details.do?cookbooksId=${os.orderId}">
   		WEB-INF/page/index/dinner/detail.html
   			211-212 行	if(confirm("请先登陆"))
							window.location.href='/index/index/my.do';
		+WEB-INF/page/index/dinner/details.html
		
		NearServiceImpl.java

			+public int getMarks(String shopId);
			+public List<ShopExt> setMarks(List<ShopExt> list);
			
			public List<ShopExt> query(int currentSize,int pageSize,String longitude,String latitude,int filterType,String filter)
			所有的 return list;之前 +list=setMarks(list);
		
		near.js
		36 行
		entershop.html
		59、77、78行
		
		Category.java  //商品分类
		
		category_id 	varchar(36); //id
		category_name	varchar(40);//分类名
		lft				int;		//左值
		rht				int;		//右值
		depth			int			//节点层次      默认为1
		
		+category		视图包
		+CategoryService.java	 
		+CategoryServiceImpl.java	 
		+Category.java
		
		表是自动建立 但要修改
		ALTER TABLE category MODIFY depth INT DEFAULT 1;
		
		测试数据
		
		INSERT INTO category(category_id,category_name,lft,rgt) VALUES('1','商品',1,18);
		INSERT INTO category(category_id,category_name,lft,rgt) VALUES('2','平板电脑',2,7);
		INSERT INTO category(category_id,category_name,lft,rgt) VALUES('3','冰箱',8,11);
		INSERT INTO category(category_id,category_name,lft,rgt) VALUES('4','笔记本',12,17);
		INSERT INTO category(category_id,category_name,lft,rgt) VALUES('5','长虹',3,4);
		INSERT INTO category(category_id,category_name,lft,rgt) VALUES('6','索尼',5,6);
		INSERT INTO category(category_id,category_name,lft,rgt) VALUES('7','西门子',9,10);
		INSERT INTO category(category_id,category_name,lft,rgt) VALUES('8','thinkpad',13,14);
		INSERT INTO category(category_id,category_name,lft,rgt) VALUES('9','dell',15,16);	 
