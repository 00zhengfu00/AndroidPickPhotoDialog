# AndroidPickPhotoDialog
### AndroidͼƬѡ��Ի���ͨ������������������ͼƬ���ɵ�ѡ���ѡ����ѡ�������Ƿ�ü�<br/>
#### ���͵�ַ��http://blog.csdn.net/ywl5320/article/details/53320945
#### ��ͼƬ�����ֲ���ʹ�õ���һ����Դ��Ŀ��https://github.com/wanliyang1990/AdViewPager
## update
����7.0ͼƬѡ��Ͳü���<br/>
�������ڶ���ѡ��ͼƬʱ����ѵ�һ��ѡ���ͼƬ��ѡ�У������ظ�ѡ��<br/>
#### ģ������̬ͼ
![image](https://github.com/wanliyang1990/AndroidPickPhotoDialog/blob/master/imgs/pickphotodialog.gif)<br/>
#### 1��ͼƬ
![image](https://github.com/wanliyang1990/AndroidPickPhotoDialog/blob/master/imgs/1.png)<br/>
#### 2��ͼƬ
![image](https://github.com/wanliyang1990/AndroidPickPhotoDialog/blob/master/imgs/2.png)<br/>
#### 3��ͼƬ
![image](https://github.com/wanliyang1990/AndroidPickPhotoDialog/blob/master/imgs/3.png)<br/>
#### 4��ͼƬ
![image](https://github.com/wanliyang1990/AndroidPickPhotoDialog/blob/master/imgs/4.png)<br/>

### ���÷�����<br/>

        private PickPhotoDialog pickPhotoDialog;
        
        //����¼��������
        pickPhotoDialog = new PickPhotoDialog(MainActivity.this, MainActivity.this);
        Window window = pickPhotoDialog.getWindow();
        window.setGravity(Gravity.BOTTOM);
        window.setWindowAnimations(R.style.DialogEnter);
        pickPhotoDialog.setCutImg(true, 5);
        pickPhotoDialog.setOnPhotoResultListener(new PickPhotoDialog.OnPhotoResultListener() {
            @Override
            public void onCameraResult(String path) {//�������ͼƬ·��
                List<ImgBean> imgBeens = new ArrayList<ImgBean>();
                ImgBean imgBean = new ImgBean();
                imgBean.setPath(path);
                imgBeens.add(imgBean);
                adViewpagerUtil = new AdViewpagerUtil(MainActivity.this, viewpager, lydots, 8, 4, imgBeens);
                adViewpagerUtil.initVps();
            }

            @Override
            public void onCutPhotoResult(Bitmap bitmap) {
                //ͼƬ(��������)�ü��󷵻ص�bitmap
            }

            @Override
            public void onPhotoResult(List<ImgBean> selectedImgs) {//����ͼѡ�񷵻�ͼƬ·�������
                if(selectedImgs != null && selectedImgs.size() > 0) {
                    adViewpagerUtil = new AdViewpagerUtil(MainActivity.this, viewpager, lydots, 8, 4, selectedImgs);
                    adViewpagerUtil.initVps();
                }
                else
                {
                    if(adViewpagerUtil != null) {
                        adViewpagerUtil.startLoopViewPager();
                    }
                }
            }
        });
        
        //Ȩ������
        @TargetApi(23)
        @Override
        public void onRequestPermissionsResult(int requestCode, String[] permissions, int[] grantResults) {
            super.onRequestPermissionsResult(requestCode, permissions, grantResults);
            if (pickPhotoDialog != null)
            {
                pickPhotoDialog.onRequestPermissionsResult(requestCode, permissions, grantResults);
            }
        }
        
        @Override
        protected void onActivityResult(int requestCode, int resultCode, Intent data) {
            // TODO Auto-generated method stub
            super.onActivityResult(requestCode, resultCode, data);
    
            if(pickPhotoDialog != null)
            {
                pickPhotoDialog.onActivityResult(requestCode, resultCode, data);
            }
        }
        

    
# create by ywl5320