# -QGraphicsScene
截取QGraphicsScene内容为图片，并可调整分辨率
/// <summary>
/// 按原分辨率渲染会卡顿因此只对50%区域进行渲染
/// </summary>
/// <param name="station"></param>
/// <param name="img"></param>
/// <param name="rectVec"></param>
//tempView为QGraphicsView对象。保存其上的scene为图片，使用QPainter进行渲染
QRectF rectf = QRectF(tempView->scene()->sceneRect());
QMarginsF marginf = QMarginsF(tempView->scene()->sceneRect().left() * 0.5, tempView->scene()->sceneRect().top() * 0.5,tempView->scene()->sceneRect().right() * 0.5, tempView->scene()->sceneRect().bottom() * 0.5);
QRectF mRectf = rectf.marginsRemoved(marginf);  //缩放0.5
//保存场景为图片
QImage viewImage = QImage(mRectf.width(), mRectf.height(), QImage::Format_RGB888);
QPainter painter(&viewImage);
tempView->scene()->render(&painter, mRectf, QRect(0, 0, tempView->scene()->sceneRect().width(), tempView->scene()->sceneRect().height()));  //渲染
painter.end();